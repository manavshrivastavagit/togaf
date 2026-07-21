# TOGAF BPMN & Process Models Repository

This document contains the core **BPMN-aligned Process Models** and flowcharts for NextGen Bank's **STP Micro-Loan Mobile Platform**. The models are represented using standard Mermaid diagram syntax, dividing workflows into clear swimlanes, tasks, decision gateways, and external integrations to provide implementation teams with a blueprint for execution.

---

## 1. Master STP Loan Origination & Disbursal Process

This swimlane-based process model illustrates the end-to-end straight-through processing lifecycle of a loan, mapping tasks across the Customer, internal microservices, and external India Stack partners.

```mermaid
flowchart TB
    %% Styling definitions
    classDef startEnd fill:#f8d7da,stroke:#dc3545,stroke-width:2px;
    classDef task fill:#cfe2ff,stroke:#0d6efd,stroke-width:1.5px;
    classDef gateway fill:#fff3cd,stroke:#ffc107,stroke-width:1.5px;
    classDef database fill:#d1e7dd,stroke:#198754,stroke-width:1.5px;
    classDef external fill:#e2e3e5,stroke:#6c757d,stroke-width:1.5px;

    subgraph UserSwim[Customer / Borrower]
        Start([Start Application]):::startEnd
        InputPAN[1. Input PAN & Mobile]:::task
        OTPReq[2. Request Aadhaar OTP]:::task
        SubmitOTP[3. Submit OTP]:::task
        SelfieStream[4. Capture Selfie Video]:::task
        AAConsent[5. Approve AA Consent OTP]:::task
        ReviewOffer[6. Review & Accept Offer]:::task
        ESignOTP[7. E-Sign Contract via OTP]:::task
        AuthMandate[8. Authorize Auto-Pay Mandate]:::task
        DisbursedSuccess([Disbursal Success]):::startEnd
    end

    subgraph AppSwim[Mobile App Client]
        EncryptLocal[Local Encrypt PII]:::task
        LivenessSDK[Trigger Liveness SDK]:::task
        RenderWebview[Render AA Webview]:::task
        ShowOffer[Render Loan Offer & KFS]:::task
        RedireSign[Redirect to e-Sign Gateway]:::task
        RedirNPCI[Redirect to UPI Pay App]:::task
    end

    subgraph GatewaySwim[API Gateway & Orchestrator]
        AuthOIDC{JWT Valid?}:::gateway
        OnbOrch[Onboarding Orchestrator]:::task
        ConsentOrch[Consent Orchestrator]:::task
    end

    subgraph EngineSwim[Credit Underwriting Engine]
        ParseAA[Parse Statement XML]:::task
        ScoreModel[Run XGBoost Risk Models]:::task
        MuleCheck{Mule Account?}:::gateway
        LimitCalc[Calculate Limit & APR]:::task
        RejectApp([Auto Reject Application]):::startEnd
    end

    subgraph LedgerSwim[LMS Ledger Core]
        LMSAccount[Create Loan Account]:::task
        GenAgreement[Generate PDF Agreement]:::task
        WriteOutbox[Write Disbursal Outbox Event]:::task
    end

    subgraph PaySwim[Payment Hub]
        IdempotentLock[Verify Idempotency Key]:::task
        DisbursalAPI[Initiate Disbursal API]:::task
    end

    subgraph ExternalSwim[External Gateways & Partners]
        CDSL[CDSL PAN Verify]:::external
        UIDAI[UIDAI e-KYC Server]:::external
        AANet[Account Aggregator API]:::external
        Bureau[CIBIL / Bureau API]:::external
        NeSL[NeSL e-Sign Portal]:::external
        NPCINet[NPCI e-Mandate Net]:::external
        SponsorBank[Sponsor Bank IMPS Gate]:::external
    end

    %% Process flow connections
    Start --> InputPAN
    InputPAN --> EncryptLocal
    EncryptLocal --> AuthOIDC
    AuthOIDC -- Yes --> OnbOrch
    OnbOrch --> CDSL
    CDSL --> OTPReq
    OTPReq --> SubmitOTP
    SubmitOTP --> OnbOrch
    OnbOrch --> UIDAI
    UIDAI --> SelfieStream
    SelfieStream --> LivenessSDK
    LivenessSDK --> OnbOrch
    OnbOrch --> ConsentOrch
    ConsentOrch --> AANet
    AANet --> RenderWebview
    RenderWebview --> AAConsent
    AAConsent --> ConsentOrch
    ConsentOrch --> ParseAA
    ParseAA --> ScoreModel
    ScoreModel --> Bureau
    ScoreModel --> MuleCheck
    MuleCheck -- Yes --> RejectApp
    MuleCheck -- No --> LimitCalc
    LimitCalc --> ShowOffer
    ShowOffer --> ReviewOffer
    ReviewOffer --> LMSAccount
    LMSAccount --> GenAgreement
    GenAgreement --> NeSL
    NeSL --> RedireSign
    RedireSign --> ESignOTP
    ESignOTP --> GenAgreement
    GenAgreement --> NPCINet
    NPCINet --> RedirNPCI
    RedirNPCI --> AuthMandate
    AuthMandate --> NPCINet
    NPCINet --> WriteOutbox
    WriteOutbox --> IdempotentLock
    IdempotentLock --> DisbursalAPI
    DisbursalAPI --> SponsorBank
    SponsorBank --> DisbursedSuccess

    %% Class assignment
    class Start,DisbursedSuccess,RejectApp startEnd;
    class InputPAN,EncryptLocal,OTPReq,SubmitOTP,SelfieStream,LivenessSDK,AAConsent,ReviewOffer,ESignOTP,AuthMandate,OnbOrch,ConsentOrch,ParseAA,ScoreModel,LimitCalc,LMSAccount,GenAgreement,WriteOutbox,IdempotentLock,DisbursalAPI task;
    class AuthOIDC,MuleCheck gateway;
    class CDSL,UIDAI,AANet,Bureau,NeSL,NPCINet,SponsorBank external;
```

---

## 2. Automated Repayment & Exception Collection Process

This flowchart details the daily lifecycle of automated repayment collections, detailing error handling and the smart dunning trigger mechanisms when payments bounce.

```mermaid
flowchart TD
    %% Styling definitions
    classDef startEnd fill:#f8d7da,stroke:#dc3545,stroke-width:2px;
    classDef task fill:#cfe2ff,stroke:#0d6efd,stroke-width:1.5px;
    classDef gateway fill:#fff3cd,stroke:#ffc107,stroke-width:1.5px;
    classDef database fill:#d1e7dd,stroke:#198754,stroke-width:1.5px;
    classDef external fill:#e2e3e5,stroke:#6c757d,stroke-width:1.5px;

    Start([Trigger Daily Repay Scheduler]):::startEnd
    QueryActive[1. Query Active Installments Due Today]:::task
    LMSDB[(PostgreSQL Ledger)]:::database
    FetchMandate[2. Fetch Registered UPI AutoPay Mandate]:::task
    SendDebit[3. Send Auto-Debit Request to NPCI]:::task
    VerifyStatus{Debit Status?}:::gateway
    
    %% Success path
    MarkPaid[4. Mark Instalment as Paid]:::task
    SendSuccessNotify[5. Send WhatsApp / SMS Confirmation]:::task
    EndSuccess([Workflow Ended - Success]):::startEnd
    
    %% Failure path (Bounce)
    LogBounce[6. Log Bounce Reason & Code]:::task
    CalculateLateFee[7. Calculate Late Fee & GST]:::task
    SendDunning[8. Trigger Smart Dunning Alert]:::task
    DunningComm[WhatsApp Notification with Instant Pay Link]:::task
    SchedulerRetry[9. Schedule Retry Event]:::task
    RetryGateway{Retry Count?}:::gateway
    
    %% Retry Escalation
    WaitDays[Wait 2 Days]:::task
    UpdateDelinquent[10. Update Loan Status to DELINQUENT]:::task
    MuleReview{Report Fraud / Bureau?}:::gateway
    BureauReport[11. Submit Negative Report to CIBIL]:::task
    Allocation[12. Refer Account to Collection API]:::task
    EndDelinquent([Workflow Ended - Delinquent]):::startEnd

    %% Process linkages
    Start --> QueryActive
    QueryActive -.-> LMSDB
    QueryActive --> FetchMandate
    FetchMandate --> SendDebit
    SendDebit --> VerifyStatus
    
    VerifyStatus -- Success --> MarkPaid
    MarkPaid -.-> LMSDB
    MarkPaid --> SendSuccessNotify
    SendSuccessNotify --> EndSuccess
    
    VerifyStatus -- Failed / Insufficient Balance --> LogBounce
    LogBounce -.-> LMSDB
    LogBounce --> CalculateLateFee
    CalculateLateFee --> SendDunning
    SendDunning --> DunningComm
    DunningComm --> SchedulerRetry
    SchedulerRetry --> RetryGateway
    
    RetryGateway -- < 3 Retries --> WaitDays
    WaitDays --> SendDebit
    
    RetryGateway -- >= 3 Retries --> UpdateDelinquent
    UpdateDelinquent -.-> LMSDB
    UpdateDelinquent --> MuleReview
    
    MuleReview -- True --> BureauReport
    BureauReport --> Allocation
    MuleReview -- False --> Allocation
    Allocation --> EndDelinquent

    %% Class assignment
    class Start,EndSuccess,EndDelinquent startEnd;
    class QueryActive,FetchMandate,SendDebit,MarkPaid,SendSuccessNotify,LogBounce,CalculateLateFee,SendDunning,DunningComm,SchedulerRetry,WaitDays,UpdateDelinquent,BureauReport,Allocation task;
    class VerifyStatus,RetryGateway,MuleReview gateway;
    class LMSDB database;
```

---

## 3. Architecture Change Management (RFC) Lifecycle

This diagram details the governance workflow for Request for Architecture Change (RFC) files. It distinguishes between Minor, Major, and Strategic shifts.

```mermaid
flowchart TD
    %% Styling definitions
    classDef startEnd fill:#f8d7da,stroke:#dc3545,stroke-width:2px;
    classDef task fill:#cfe2ff,stroke:#0d6efd,stroke-width:1.5px;
    classDef gateway fill:#fff3cd,stroke:#ffc107,stroke-width:1.5px;

    Start([Identify Change Need]):::startEnd
    DraftRFC[1. Draft RFC Document]:::task
    ClassifyChange{Change Severity?}:::gateway
    
    %% Minor Change path
    DevLeadApprove[2a. Dev Lead Approval & commit log]:::task
    EndMinor([Apply Minor Update]):::startEnd
    
    %% Major Change path
    EAImpact[2b. EA Impact Analysis]:::task
    EASignOff{EA Review Approval?}:::gateway
    UpdateRepo[3. Update Architecture Docs & task.md]:::task
    DeployCode[4. Deploy Code via CI/CD]:::task
    EndChange([Workflow Completed]):::startEnd
    
    %% Strategic Change path
    BoardReview[2c. Formal Architecture Board Presentation]:::task
    BoardVote{Board Consensus?}:::gateway
    ReDraft[Modify proposal]:::task

    %% Flow connections
    Start --> DraftRFC
    DraftRFC --> ClassifyChange
    
    ClassifyChange -- Minor --> DevLeadApprove
    DevLeadApprove --> EndMinor
    
    ClassifyChange -- Major --> EAImpact
    EAImpact --> EASignOff
    EASignOff -- Yes --> UpdateRepo
    EASignOff -- No --> ReDraft
    
    ClassifyChange -- Strategic --> BoardReview
    BoardReview --> BoardVote
    BoardVote -- Approved --> UpdateRepo
    BoardVote -- Rejected --> ReDraft
    
    ReDraft --> DraftRFC
    UpdateRepo --> DeployCode
    DeployCode --> EndChange

    %% Class assignment
    class Start,EndMinor,EndChange startEnd;
    class DraftRFC,DevLeadApprove,EAImpact,UpdateRepo,DeployCode,BoardReview,ReDraft task;
    class ClassifyChange,EASignOff,BoardVote gateway;
```

---

## 4. Architecture Waiver Management Workflow

This flowchart maps the process of submitting, evaluating, approving, and auditing architecture waivers.

```mermaid
flowchart TD
    %% Styling definitions
    classDef startEnd fill:#f8d7da,stroke:#dc3545,stroke-width:2px;
    classDef task fill:#cfe2ff,stroke:#0d6efd,stroke-width:1.5px;
    classDef gateway fill:#fff3cd,stroke:#ffc107,stroke-width:1.5px;

    Start([Identify Architecture Deviation]):::startEnd
    SubmitWaiver[1. Submit Waiver Form with Rationale & Remediation Plan]:::task
    EAEval[2. Lead Architect Compliance & Risk Evaluation]:::task
    IsRegulatory{RBI DLG / Security Violation?}:::gateway
    AutoReject[3. Auto-Reject Waiver & Block Release]:::task
    EndReject([Remediation Required]):::startEnd
    
    BoardReview[4. Present to Architecture Board]:::task
    BoardDecision{Board Decision?}:::gateway
    WaiverApproved[5a. Approved: Log Waiver & Update task.md]:::task
    DeployWaiver[6. Deploy with Temporary Waiver active]:::task
    ScheduledAudit[7. Monitor Remediation Schedule < 180 Days]:::task
    AuditPassed{Remediated?}:::gateway
    EndSuccess([Waiver Closed - Fully Compliant]):::startEnd

    %% Flow connections
    Start --> SubmitWaiver
    SubmitWaiver --> EAEval
    EAEval --> IsRegulatory
    
    IsRegulatory -- Yes --> AutoReject
    AutoReject --> EndReject
    
    IsRegulatory -- No --> BoardReview
    BoardReview --> BoardDecision
    
    BoardDecision -- Rejected --> AutoReject
    BoardDecision -- Approved --> WaiverApproved
    
    WaiverApproved --> DeployWaiver
    DeployWaiver --> ScheduledAudit
    ScheduledAudit --> AuditPassed
    
    AuditPassed -- Yes --> EndSuccess
    AuditPassed -- No --> AutoReject

    %% Class assignment
    class Start,EndReject,EndSuccess startEnd;
    class SubmitWaiver,EAEval,AutoReject,BoardReview,WaiverApproved,DeployWaiver,ScheduledAudit task;
    class IsRegulatory,BoardDecision,AuditPassed gateway;
```
