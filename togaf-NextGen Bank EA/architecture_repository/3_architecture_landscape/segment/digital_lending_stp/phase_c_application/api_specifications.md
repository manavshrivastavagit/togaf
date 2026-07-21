# Phase C: Application Architecture - API Specifications

This document defines the REST API contract for the primary application entry points, complying with OpenAPI 3.0 specifications.

---

## 1. OpenAPI 3.0 Specification (YAML)

```yaml
openapi: 3.0.3
info:
  title: Digital Lending Platform API
  description: API specifications for Customer Onboarding, Consent Management, Underwriting, and Disbursement.
  version: 1.0.0
servers:
  - url: https://api.digital-lender.com/api/v1
    description: Production API Gateway
paths:
  /onboard:
    post:
      summary: Initiate Customer Onboarding
      description: Captures primary customer detail, validates details, and verifies PAN.
      operationId: onboardCustomer
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/OnboardRequest'
      responses:
        '201':
          description: Onboarding profile initialized successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/OnboardResponse'
        '400':
          description: Validation error or invalid phone/PAN formatting.
        '409':
          description: Duplicate registration detected.

  /consent:
    post:
      summary: Request Account Aggregator Consent
      description: Initiates a consent handle request for retrieving customer bank statements.
      operationId: initiateConsent
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ConsentRequest'
      responses:
        '200':
          description: Consent request created, redirect URL to AA app generated.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ConsentResponse'
        '404':
          description: Customer ID not found.

  /underwrite/assess:
    post:
      summary: Risk Assessment and Underwriting
      description: Triggers underwriting models using retrieved AA bank statement payload.
      operationId: assessUnderwriting
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UnderwriteRequest'
      responses:
        '200':
          description: Underwriting assessment complete.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UnderwriteResponse'
        '422':
          description: Bank statement parsing failed or insufficient data for assessment.

  /loan/disburse:
    post:
      summary: Disburse Loan Principal
      description: Triggers disbursement workflow to pay approved principal to target bank account.
      operationId: disburseLoan
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/DisburseRequest'
      responses:
        '202':
          description: Disbursement transaction accepted and sent for processing.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/DisburseResponse'
        '412':
          description: Pre-conditions failed (e.g. Mandate active check failed).

components:
  schemas:
    OnboardRequest:
      type: object
      required:
        - fullName
        - pan
        - mobileNumber
        - email
        - dob
        - aadhaarVaultRef
      properties:
        fullName:
          type: string
          example: "Manav Shrivastava"
        pan:
          type: string
          pattern: '^[A-Z]{5}[0-9]{4}[A-Z]{1}$'
          example: "ABCDE1234F"
        mobileNumber:
          type: string
          pattern: '^\+[1-9]\d{1,14}$'
          example: "+919999999999"
        email:
          type: string
          format: email
          example: "manav@example.com"
        dob:
          type: string
          format: date
          example: "1994-05-15"
        aadhaarVaultRef:
          type: string
          format: uuid
          example: "f81d4fae-7dec-11d0-a765-00a0c91e6bf6"

    OnboardResponse:
      type: object
      properties:
        customerId:
          type: string
          format: uuid
          example: "d3b07384-d113-4956-b519-e58eb3860bb4"
        kycStatus:
          type: string
          enum: [PENDING, APPROVED, SUSPENDED]
          example: "APPROVED"
        createdAt:
          type: string
          format: date-time
          example: "2026-05-21T17:20:00Z"

    ConsentRequest:
      type: object
      required:
        - customerId
        - aaHandle
        - dataRangeFrom
        - dataRangeTo
      properties:
        customerId:
          type: string
          format: uuid
          example: "d3b07384-d113-4956-b519-e58eb3860bb4"
        aaHandle:
          type: string
          example: "manav@xyz-aa"
        dataRangeFrom:
          type: string
          format: date
          example: "2025-11-01"
        dataRangeTo:
          type: string
          format: date
          example: "2026-05-01"

    ConsentResponse:
      type: object
      properties:
        consentId:
          type: string
          format: uuid
          example: "6c9d08ee-53d9-43c2-a9b3-6c8f94cb1234"
        consentHandle:
          type: string
          example: "aa-txn-handle-7778"
        redirectUrl:
          type: string
          format: uri
          example: "https://app.xyz-aa.in/consent/approve?handle=aa-txn-handle-7778"

    UnderwriteRequest:
      type: object
      required:
        - applicationId
        - consentId
      properties:
        applicationId:
          type: string
          format: uuid
          example: "2a2a2a2a-2a2a-2a2a-2a2a-2a2a2a2a2a2a"
        consentId:
          type: string
          format: uuid
          example: "6c9d08ee-53d9-43c2-a9b3-6c8f94cb1234"

    UnderwriteResponse:
      type: object
      properties:
        applicationId:
          type: string
          format: uuid
        decision:
          type: string
          enum: [APPROVED, REJECTED, MANUAL_REVIEW]
          example: "APPROVED"
        creditScore:
          type: integer
          example: 780
        approvedLimit:
          type: number
          example: 500000.00
        interestRate:
          type: number
          example: 12.50
        reason:
          type: string
          example: "Consistent positive cash flows, low debt-to-income ratio."

    DisburseRequest:
      type: object
      required:
        - applicationId
        - bankAccountNumber
        - ifscCode
        - mandateId
      properties:
        applicationId:
          type: string
          format: uuid
          example: "2a2a2a2a-2a2a-2a2a-2a2a-2a2a2a2a2a2a"
        bankAccountNumber:
          type: string
          example: "1234567890"
        ifscCode:
          type: string
          example: "HDFC0000123"
        mandateId:
          type: string
          format: uuid
          example: "4c4c4c4c-4c4c-4c4c-4c4c-4c4c4c4c4c4c"

    DisburseResponse:
      type: object
      properties:
        transactionRef:
          type: string
          example: "TXN123456789"
        loanAccountId:
          type: string
          format: uuid
          example: "5d5d5d5d-5d5d-5d5d-5d5d-5d5d5d5d5d5d"
        status:
          type: string
          enum: [INITIATED, PROCESSING, COMPLETED, FAILED]
          example: "INITIATED"
        message:
          type: string
          example: "Payout initiated to target bank account via IMPS."
```
