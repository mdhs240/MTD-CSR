# MTD CSR PLATFORM - DATA DICTIONARY

### **5-Role System**
- `admin`: Full system access
- `accountant`: Financial management
- `project_manager`: Project oversight
- `team_member`: Execution tasks
- `client`: Read-only external access

  
## Complete Field-Level Documentation for All Tables

---

## 1. USERS
**Purpose:** Manages user accounts linked to Supabase auth

**Fields:**
- `id`: Unique user identifier (UUID from auth)
- `email`: Login email (unique)
- `full_name`: Display name
- `mobile_number`: Primary contact
- `alternate_mobile`: Backup contact
- `address, city, state, pincode`: Personal address
- `role`: Access level (client/project_manager/accountant/admin/team_member)
- `department, team, designation`: Org structure
- `manager_id, reporting_to`: Hierarchy links
- `avatar_drive_link`: Profile photo (Google Drive)
- `date_of_joining`: Employment start
- `employee_id`: HR ID (unique)
- `is_active`: Account status
- `last_login_at`: Security tracking
- `preferences, permissions`: UI & access customization (JSONB)
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by, updated_by`: Audit trail

---

## 2. CSR_PARTNERS
**Purpose:** Corporate Social Responsibility partners/clients providing funding

**Fields:**
- `id`: Unique partner identifier (UUID)
- `name`: Partner organization name
- `company_name`: Legal entity name
- `registration_number`: Company registration ID
- `pan_number`: Tax identification (PAN)
- `gst_number`: GST registration
- `contact_person`: Primary contact name
- `designation`: Contact's job title
- `email`: Partner email
- `phone, alternate_phone`: Contact numbers
- `address, city, state, pincode`: Office location
- `website`: Partner website URL
- `logo_drive_link`: Company logo (Google Drive)
- `mou_drive_link`: Memorandum of Understanding document (Google Drive)
- `budget_allocated`: Total budget from partner
- `budget_utilized`: Amount already spent
- `budget_pending`: Amount in pending expenses
- `fiscal_year`: Budget period
- `agreement_start_date, agreement_end_date`: Contract validity
- `payment_terms`: Payment conditions
- `billing_cycle`: Invoice frequency
- `bank_details`: Banking info for payments (JSONB)
- `contact_details`: Multiple contacts array (JSONB)
- `documents`: All partner documents (JSONB array of Drive links)
- `is_active`: Partner status
- `notes`: Additional remarks
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by, updated_by`: Audit trail

---

## 3. PROJECTS
**Purpose:** Highly detailed project tracking with complete interconnections

**Fields:**
- `id`: Unique project identifier (UUID)
- `project_code`: Human-readable unique code
- `name`: Project title
- `description`: Detailed project info
- `csr_partner_id`: Link to funding partner
- `project_manager_id`: Primary manager
- `assistant_manager_id`: Secondary manager
- `location`: General location
- `state, district, city, block, village, pincode`: Detailed address
- `latitude, longitude`: GPS coordinates
- `category, sub_category`: Project classification
- `project_type`: One-time/Ongoing/Recurring
- `focus_area`: Areas of work (Array)
- `sdg_goals`: UN Sustainable Development Goals (Array)
- `status`: Current phase (planning/active/on_hold/completed/cancelled/archived)
- `start_date, expected_end_date, actual_end_date`: Timeline
- `duration_months`: Project length
- `total_budget`: Sanctioned amount
- `approved_budget`: Approved amount
- `utilized_budget`: Spent amount (auto-calculated)
- `pending_budget`: In-process expenses (auto-calculated)
- `contingency_budget`: Emergency funds
- `total_beneficiaries, direct_beneficiaries, indirect_beneficiaries`: Impact numbers
- `male_beneficiaries, female_beneficiaries, children_beneficiaries`: Demographics
- `beneficiaries_reached`: Actual reach
- `targets, achievements`: Goals vs results (JSONB)
- `proposal_drive_link`: Project proposal (Google Drive)
- `approval_letter_drive_link`: Sanction letter (Google Drive)
- `budget_sheet_drive_link`: Budget breakdown (Google Drive)
- `mou_drive_link`: Agreement (Google Drive)
- `project_plan_drive_link`: Detailed plan (Google Drive)
- `documents_folder_link`: Main documents folder (Google Drive)
- `completion_percentage`: Progress (0-100, auto-calculated)
- `milestones_completed, total_milestones`: Milestone tracking
- `risks, issues`: Risk & issue log (JSONB arrays)
- `compliance_status`: Regulatory compliance
- `last_audit_date, next_audit_date`: Audit schedule
- `is_active`: Project status
- `is_confidential`: Data sensitivity flag
- `priority`: Urgency level (low/normal/high/urgent/critical)
- `tags`: Searchable keywords (Array)
- `notes`: Additional remarks
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by, updated_by`: Audit trail

---

## 4. PROJECT_TEAM_MEMBERS
**Purpose:** Detailed team member assignments per project

**Fields:**
- `id`: Unique assignment identifier (UUID)
- `project_id`: Link to project
- `user_id`: Link to team member
- `role`: Project-specific role
- `designation`: Job title in project
- `responsibilities`: Role description
- `allocation_percentage`: Time allocation (0-100%)
- `is_lead`: Lead position flag
- `can_approve_expenses`: Expense approval permission
- `can_assign_tasks`: Task assignment permission
- `access_level`: Data access (full/limited/view_only)
- `assigned_date`: Joining date
- `removed_date`: Exit date
- `is_active`: Current status
- `notes`: Additional remarks
- `created_at, updated_at, created_by, updated_by`: Audit trail

---

## 5. PROJECT_STAKEHOLDERS
**Purpose:** External contacts and stakeholders per project

**Fields:**
- `id`: Unique stakeholder identifier (UUID)
- `project_id`: Link to project
- `name`: Stakeholder name
- `organization`: Affiliated org
- `designation`: Job title
- `stakeholder_type`: Category (Government/NGO/Community Leader/Vendor)
- `email, phone`: Contact details
- `address`: Location
- `role_in_project`: Project involvement
- `influence_level`: Impact level (High/Medium/Low)
- `engagement_level`: Participation (Active/Moderate/Passive)
- `communication_preference`: Preferred contact method
- `notes`: Additional remarks
- `is_active`: Current status
- `created_at, updated_at, created_by`: Audit trail

---

## 6. TIMELINES
**Purpose:** Project milestones and deliverables with dependencies

**Fields:**
- `id`: Unique milestone identifier (UUID)
- `project_id`: Link to project
- `parent_id`: Sub-milestone hierarchy
- `milestone_code`: Unique code
- `title`: Milestone name
- `description`: Detailed info
- `category`: Phase (Planning/Execution/Monitoring/Closure)
- `start_date, end_date`: Planned dates
- `actual_start_date, actual_end_date`: Actual dates
- `duration_days`: Length in days
- `status`: Current state (not_started/in_progress/completed/on_priority/blocked/cancelled)
- `completion_percentage`: Progress (0-100)
- `order_index`: Sequence number
- `priority`: Urgency level
- `is_critical_path`: Critical path flag
- `dependencies`: Dependent milestone IDs (Array)
- `deliverables`: Expected outputs (Array)
- `success_criteria`: Completion criteria (Array)
- `responsible_user_id`: Owner
- `approved_by, approval_date`: Approval details
- `notes`: Additional remarks
- `attachments`: Supporting docs (JSONB array of Drive links)
- `created_at, updated_at, created_by, updated_by`: Audit trail

---

## 7. TASKS
**Purpose:** Highly detailed task management with complete tracking

**Fields:**
- `id`: Unique task identifier (UUID)
- `task_code`: Human-readable unique code
- `project_id`: Link to project
- `timeline_id`: Link to milestone
- `parent_task_id`: Sub-task hierarchy
- `title`: Task name
- `description`: Detailed info
- `task_type`: Category (Development/Research/Meeting/Review)
- `category`: Classification
- `assigned_to`: Task owner
- `assigned_by`: Task creator
- `reviewer_id`: Reviewer
- `status`: Current state (not_started/in_progress/completed/on_priority/blocked/cancelled)
- `priority`: Urgency level
- `completion_percentage`: Progress (0-100)
- `estimated_hours`: Planned effort
- `actual_hours`: Logged time (auto-calculated)
- `due_date`: Deadline
- `start_date, completed_date`: Actual dates
- `department`: Responsible dept
- `tags`: Keywords (Array)
- `dependencies`: Dependent task IDs (Array)
- `blockers`: Blocking issues (Array)
- `location, latitude, longitude`: Field task location
- `is_visible_to_client`: Client visibility
- `is_from_client_timeline`: Client-requested flag
- `checklist`: Sub-tasks (JSONB array)
- `attachments`: Task files (JSONB array of Drive links)
- `comments_count, updates_count`: Interaction metrics (auto-calculated)
- `notes`: Additional remarks
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by, updated_by`: Audit trail

---

## 8. TASK_COMMENTS
**Purpose:** Thread-based communication on tasks

**Fields:**
- `id`: Unique comment identifier (UUID)
- `task_id`: Link to task
- `user_id`: Comment author
- `parent_comment_id`: Reply thread hierarchy
- `comment_text`: Comment content
- `attachments`: Comment files (JSONB array of Drive links)
- `mentions`: Tagged user IDs (Array)
- `is_internal`: Internal team only flag
- `is_edited`: Edit flag
- `edited_at`: Last edit timestamp
- `created_at`: Comment timestamp

---

## 9. TASK_TIME_LOGS
**Purpose:** Detailed time tracking per task

**Fields:**
- `id`: Unique log identifier (UUID)
- `task_id`: Link to task
- `user_id`: Time logger
- `start_time`: Work start
- `end_time`: Work end
- `duration_minutes`: Total time (auto-calculated)
- `description`: Work description
- `is_billable`: Billable hours flag
- `created_at`: Log timestamp

---

## 10. REAL_TIME_UPDATES
**Purpose:** Project progress updates with media and location tracking

**Fields:**
- `id`: Unique update identifier (UUID)
- `update_code`: Human-readable unique code
- `project_id`: Link to project
- `task_id`: Link to task (optional)
- `timeline_id`: Link to milestone (optional)
- `title`: Update heading
- `description`: Detailed update
- `update_type`: Category (Progress/Issue/Achievement/Milestone)
- `category`: Classification
- `update_number`: Sequence number
- `document_number`: Reference ID
- `reference_number`: External reference
- `date, time`: Update timestamp
- `location_name, school_name, institution_name`: Location details
- `address, city, state`: Location address
- `latitude, longitude`: GPS coordinates
- `images`: Photo array (JSONB array of Drive links)
- `videos`: Video array (JSONB array of Drive links)
- `documents`: Document array (JSONB array of Drive links)
- `participants`: Involved user IDs (Array)
- `beneficiaries_count, attendees_count`: Participation numbers
- `impact_data`: Impact metrics (JSONB)
- `metrics`: Quantitative data (JSONB)
- `is_public`: Public visibility flag
- `is_featured`: Featured flag
- `is_sent_to_client`: Client sharing flag
- `sent_date`: Sharing timestamp
- `format_type`: Update format
- `tags`: Keywords (Array)
- `notes`: Additional remarks
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by, updated_by`: Audit trail

---

## 11. MEDIA_ARTICLES
**Purpose:** Media library - ONLY Google Drive links stored (NO actual files uploaded to Supabase)

**Fields:**
- `id`: Unique media identifier (UUID)
- `media_code`: Human-readable unique code
- `project_id`: Link to project
- `task_id`: Link to task (optional)
- `update_id`: Link to update (optional)
- `title`: Media title
- `description`: Media description
- `media_type`: File type (photo/video/document/pdf/newspaper_cutting/certificate/report)
- `category, sub_category`: Classification
- `drive_link`: Main file link (Google Drive) - **PRIMARY & ONLY STORAGE**
- `drive_folder_link`: Folder link for multiple files (Google Drive)
- `thumbnail_link`: Preview image (Google Drive)
- `file_name`: Original filename (reference only)
- `file_size_mb`: File size (reference only)
- `file_format`: Extension (reference only)
- `resolution`: Image/video quality (metadata only)
- `duration_seconds`: Video length (metadata only)
- `is_geo_tagged`: GPS data flag
- `latitude, longitude`: GPS coordinates
- `captured_at`: Photo/video timestamp (metadata)
- `camera_details`: Camera info (metadata)
- `news_channel`: For news items
- `publication_name`: For articles
- `publication_date`: Publishing date
- `reporter_name`: Journalist name
- `article_url`: Online article link
- `date`: Entry date
- `event_date`: Event date
- `location`: Location name
- `tags, keywords`: Searchable terms (Arrays)
- `is_public`: Public access flag
- `is_downloadable`: Download permission (from Drive)
- `access_level`: Access control (public/client/internal/restricted)
- `uploaded_by`: User who added the Drive link
- `approved_by, approval_date`: Approval details
- `views_count, downloads_count`: Usage metrics
- `notes`: Additional remarks
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by`: Audit trail

**⚠️ IMPORTANT:** This table stores ONLY Google Drive links, NOT actual media files. All photos, videos, PDFs are stored in Google Drive.

---

## 12. EXPENSE_CATEGORIES
**Purpose:** Hierarchical expense classification

**Fields:**
- `id`: Unique category identifier (UUID)
- `name`: Category name (unique)
- `code`: Category code (unique)
- `parent_category_id`: Hierarchy link
- `description`: Category details
- `budget_limit`: Category budget cap
- `requires_approval`: Approval requirement flag
- `approval_limit`: Auto-approval threshold
- `is_active`: Category status
- `created_at`: Creation timestamp

---

## 13. PROJECT_EXPENSES
**Purpose:** Extremely detailed expense tracking with approval workflow - ALL documents via Google Drive

**Fields:**
- `id`: Unique expense identifier (UUID)
- `expense_code`: Human-readable unique code
- `project_id`: Link to project
- `category_id`: Link to expense category
- `task_id`: Link to task (optional)
- `merchant_name`: Vendor name
- `merchant_contact, merchant_address`: Vendor details
- `merchant_gstin, merchant_pan`: Vendor tax IDs
- `date`: Expense date
- `category, sub_category`: Classification
- `description`: Expense details
- `purpose`: Expense reason
- `base_amount`: Pre-tax amount
- `tax_amount`: Total tax
- `gst_percentage`: GST rate
- `cgst_amount, sgst_amount, igst_amount`: GST breakdown
- `other_charges`: Additional fees
- `discount_amount`: Discounts
- `total_amount`: Final amount
- `payment_method`: Payment mode (Cash/Cheque/Online/Card)
- `payment_reference`: Transaction ID
- `payment_date`: Payment date
- `paid_to`: Payee name
- `bank_details`: Payment bank info (JSONB)
- `bill_drive_link`: Main bill (Google Drive)
- `invoice_drive_link`: Invoice (Google Drive)
- `receipt_drive_link`: Payment receipt (Google Drive)
- `supporting_docs`: Additional docs (JSONB array of Drive links)
- `status`: Workflow state (draft/submitted/pending/approved/rejected/reimbursed)
- `submitted_by`: Submitter
- `submitted_date`: Submission date
- `reviewed_by, reviewed_date`: Review details
- `approved_by, approved_date`: Approval details
- `rejection_reason`: If rejected
- `reimbursed_date`: Payment date
- `account_code, gl_code, cost_center`: Accounting codes
- `is_reimbursable`: Reimbursement flag
- `reimbursed_to`: Reimbursement recipient
- `approval_chain`: Approval workflow (JSONB array)
- `current_approver`: Current approver
- `priority`: Urgency level
- `tags`: Keywords (Array)
- `notes`: Remarks
- `internal_notes`: Private notes (not visible to submitter)
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by, updated_by`: Audit trail

---

## 14. EXPENSE_APPROVALS
**Purpose:** Expense approval audit log

**Fields:**
- `id`: Unique approval log identifier (UUID)
- `expense_id`: Link to expense
- `approver_id`: Approver user
- `action`: Action taken (submitted/approved/rejected/requested_changes)
- `previous_status`: Before status
- `new_status`: After status
- `comments`: Approval remarks
- `attachments`: Supporting files (JSONB array of Drive links)
- `created_at`: Action timestamp

---

## 15. BUDGET_ALLOCATION
**Purpose:** Detailed budget tracking by category

**Fields:**
- `id`: Unique allocation identifier (UUID)
- `project_id`: Link to project
- `category_id`: Link to expense category
- `category_name`: Category name
- `allocated_amount`: Budgeted amount
- `utilized_amount`: Spent amount (auto-calculated)
- `pending_amount`: In-process amount
- `available_amount`: Remaining balance
- `fiscal_year, quarter, month`: Time period
- `notes`: Additional remarks
- `created_at, updated_at`: Audit trail

---

## 16. BUDGET_UTILIZATION
**Purpose:** Partner-wise CSR budget tracking

**Fields:**
- `id`: Unique utilization identifier (UUID)
- `csr_partner_id`: Link to partner
- `project_id`: Link to project
- `fiscal_year, quarter, month`: Time period
- `allocated_amount`: Sanctioned budget
- `utilized_amount`: Spent amount
- `committed_amount`: Approved but not paid
- `pending_amount`: Awaiting approval
- `available_amount`: Remaining balance
- `utilization_percentage`: Usage % (auto-calculated)
- `date`: Record date
- `description`: Utilization details
- `notes`: Additional remarks
- `created_at, updated_at, created_by, updated_by`: Audit trail

---

## 17. UTILIZATION_CERTIFICATES
**Purpose:** Official utilization certificates for partners

**Fields:**
- `id`: Unique certificate identifier (UUID)
- `certificate_code`: Human-readable unique code
- `project_id`: Link to project
- `csr_partner_id`: Link to partner
- `certificate_heading`: Certificate title
- `certificate_type`: Type (Quarterly/Annual/Project Completion)
- `period_from, period_to`: Covered period
- `fiscal_year`: Financial year
- `total_amount`: Total sanctioned
- `utilized_amount`: Amount utilized
- `certificate_drive_link`: Main UC document (Google Drive)
- `annexure_drive_link`: Annexure (Google Drive)
- `supporting_docs`: Supporting docs (JSONB array of Drive links)
- `format_type`: Certificate format
- `issue_date`: Issuance date
- `prepared_by, reviewed_by, approved_by`: Workflow users
- `status`: Certificate status (draft/pending/approved)
- `sent_to_partner`: Sharing flag
- `sent_date`: Sharing date
- `acknowledged`: Partner acknowledgment flag
- `acknowledgment_date`: Acknowledgment date
- `notes`: Additional remarks
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by, updated_by`: Audit trail

---

## 18. BILLS
**Purpose:** Bill and invoice management

**Fields:**
- `id`: Unique bill identifier (UUID)
- `bill_code`: Human-readable unique code
- `project_id`: Link to project
- `expense_id`: Link to expense (optional)
- `bill_overview`: Bill summary
- `bill_type`: Type (Invoice/Receipt/Estimate)
- `bill_number`: Vendor bill number
- `vendor_name`: Vendor name
- `vendor_gstin`: Vendor GST
- `date`: Bill date
- `due_date`: Payment due date
- `subtotal`: Pre-tax amount
- `tax_amount`: Total tax
- `total_amount`: Final amount
- `amount_paid`: Paid amount
- `balance_amount`: Outstanding balance
- `status`: Payment status (pending/approved/paid)
- `bill_drive_link`: Bill document (Google Drive)
- `payment_terms`: Payment conditions
- `payment_method`: Payment mode
- `payment_reference`: Transaction ID
- `submitted_by, approved_by, paid_by`: Workflow users
- `notes`: Additional remarks
- `created_at, updated_at, created_by`: Audit trail

---

## 19. REPORTS
**Purpose:** Comprehensive report generation and management

**Fields:**
- `id`: Unique report identifier (UUID)
- `report_code`: Human-readable unique code
- `project_id`: Link to project (optional)
- `title`: Report title
- `report_type`: Type (Project/Daily/Monthly/Quarterly/Annual/Impact/Financial)
- `category`: Classification
- `description`: Report overview
- `summary`: Executive summary
- `period_from, period_to`: Covered period
- `fiscal_year`: Financial year
- `report_drive_link`: Main report (Google Drive)
- `presentation_drive_link`: Presentation (Google Drive)
- `annexures_drive_link`: Supporting docs (Google Drive)
- `status`: Report status (draft/in_review/submitted/approved/rejected)
- `generated_by, reviewed_by, approved_by`: Workflow users
- `generated_date, submitted_date, approved_date`: Workflow dates
- `data`: Report data (JSONB)
- `charts`: Chart configurations (JSONB array)
- `metrics`: Key metrics (JSONB)
- `is_public`: Public access flag
- `is_sent_to_client`: Client sharing flag
- `sent_date`: Sharing date
- `version`: Version number
- `parent_report_id`: Version history link
- `tags`: Keywords (Array)
- `notes`: Additional remarks
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by, updated_by`: Audit trail

---

## 20. DAILY_REPORTS
**Purpose:** Field activity and daily work reports

**Fields:**
- `id`: Unique report identifier (UUID)
- `report_code`: Human-readable unique code
- `project_id`: Link to project
- `user_id`: Report author
- `date`: Report date
- `day_of_week`: Day name
- `work_summary`: Daily summary
- `activities`: Activity list (Array)
- `locations_visited`: Locations (Array)
- `tasks_completed, tasks_pending, tasks_started`: Task metrics
- `task_details`: Task breakdown (JSONB array)
- `meetings_count`: Meeting count
- `meetings_details`: Meeting info (JSONB array)
- `people_met`: People contacted (Array)
- `travel_details`: Travel info
- `distance_km`: Distance traveled
- `travel_expenses`: Travel cost
- `challenges`: Issues faced
- `issues_faced`: Issue list (Array)
- `next_steps`: Next actions
- `support_required`: Help needed
- `hours_worked`: Work hours
- `start_time, end_time`: Work timing
- `photos, videos, documents`: Media (JSONB arrays of Drive links)
- `notes`: Additional remarks
- `submitted_at`: Submission timestamp
- `approved_by, approved_at`: Approval details
- `created_at, updated_at`: Audit trail

---

## 21. DATA_ENTRY_FORMS
**Purpose:** Survey, assessment, and data collection forms

**Fields:**
- `id`: Unique form identifier (UUID)
- `form_code`: Human-readable unique code
- `project_id`: Link to project
- `form_name`: Form title
- `form_type`: Type (Survey/Assessment/Feedback/Registration)
- `template_id`: Form template link
- `date`: Form date
- `location, school_name, institution_name`: Location details
- `pre_form_data`: Baseline data (JSONB)
- `post_form_data`: Post-intervention data (JSONB)
- `responses`: Form responses (JSONB)
- `respondent_name`: Respondent name
- `respondent_type`: Respondent category
- `respondent_count`: Number of respondents
- `filled_form_drive_link`: Filled form (Google Drive)
- `scanned_form_drive_link`: Scanned form (Google Drive)
- `submitted_by, verified_by`: Workflow users
- `status`: Form status (draft/submitted/verified)
- `notes`: Additional remarks
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by`: Audit trail

---

## 22. CALENDAR_EVENTS
**Purpose:** Event and meeting scheduling with attendance tracking

**Fields:**
- `id`: Unique event identifier (UUID)
- `event_code`: Human-readable unique code
- `project_id`: Link to project (optional)
- `task_id`: Link to task (optional)
- `title`: Event title
- `description`: Event details
- `event_type`: Type (Meeting/Training/Workshop/Review/Field Visit)
- `category`: Classification
- `event_date`: Event date
- `start_time, end_time`: Event timing
- `duration_minutes`: Duration
- `is_all_day`: All-day event flag
- `location, venue`: Location details
- `meeting_link`: Online meeting URL
- `latitude, longitude`: GPS coordinates
- `organizer_id`: Event organizer
- `assigned_to`: Invited user IDs (Array)
- `participants`: Participant details (JSONB array)
- `expected_attendees, actual_attendees`: Attendance numbers
- `is_recurring`: Recurring event flag
- `recurrence_pattern`: Recurrence rule
- `recurrence_end_date`: Recurrence end
- `reminders`: Reminder settings (JSONB array)
- `status`: Event status (scheduled/ongoing/completed/cancelled)
- `is_mandatory`: Mandatory attendance flag
- `agenda`: Meeting agenda
- `minutes`: Meeting minutes
- `action_items`: Action items (JSONB array)
- `documents`: Event docs (JSONB array of Drive links)
- `notes`: Additional remarks
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by, updated_by`: Audit trail

---

## 23. EVENT_ATTENDANCE
**Purpose:** Track attendance for calendar events

**Fields:**
- `id`: Unique attendance identifier (UUID)
- `event_id`: Link to event
- `user_id`: Attendee user
- `status`: Attendance status (invited/accepted/declined/attended/absent)
- `response_date`: RSVP date
- `check_in_time`: Arrival time
- `check_out_time`: Departure time
- `notes`: Additional remarks
- `created_at`: Record timestamp

---

## 24. NOTIFICATIONS
**Purpose:** In-app notifications and alerts

**Fields:**
- `id`: Unique notification identifier (UUID)
- `user_id`: Recipient user
- `title`: Notification title
- `message`: Notification message
- `notification_type`: Type (task/expense/project/system/alert)
- `category`: Classification
- `priority`: Urgency level
- `reference_type`: Referenced entity type (task/expense/project/report)
- `reference_id`: Referenced entity ID
- `project_id`: Link to project (optional)
- `action_url`: Click action URL
- `action_text`: Action button text
- `requires_action`: Action required flag
- `channels`: Delivery channels (in_app/email/whatsapp/sms) (Array)
- `is_read`: Read flag
- `read_at`: Read timestamp
- `is_seen`: Seen flag
- `seen_at`: Seen timestamp
- `scheduled_for`: Schedule time
- `sent_at`: Sent timestamp
- `expires_at`: Expiry time
- `metadata`: Extra data (JSONB)
- `created_at, created_by`: Audit trail

---

## 25. COMMUNICATIONS
**Purpose:** Complete communication history tracking

**Fields:**
- `id`: Unique communication identifier (UUID)
- `project_id`: Link to project (optional)
- `task_id`: Link to task (optional)
- `event_id`: Link to event (optional)
- `communication_type`: Type (email/whatsapp/phone/meeting/system)
- `from_user_id`: Sender
- `to_user_id`: Recipient
- `cc_users, bcc_users`: CC/BCC users (Arrays)
- `subject`: Communication subject
- `message`: Communication message
- `call_duration_minutes`: For phone calls
- `call_outcome`: Call result
- `meeting_notes`: For meetings
- `attendees`: Meeting attendees (Array)
- `attachments`: Communication files (JSONB array of Drive links)
- `status`: Delivery status (sent/delivered/read/replied/failed)
- `sent_at, delivered_at, read_at`: Status timestamps
- `is_internal`: Internal communication flag
- `priority`: Urgency level
- `metadata`: Extra data (JSONB)
- `created_at, created_by`: Audit trail

---

## 26. EMAIL_TEMPLATES
**Purpose:** Reusable email templates for automated notifications

**Fields:**
- `id`: Unique template identifier (UUID)
- `name`: Template name (unique)
- `subject`: Email subject
- `body`: Email body (HTML supported)
- `category`: Template category
- `variables`: Template variables (JSONB array)
- `is_active`: Template status
- `created_at, updated_at`: Audit trail

---

## 27. WHATSAPP_TEMPLATES
**Purpose:** Reusable WhatsApp message templates for automated notifications

**Fields:**
- `id`: Unique template identifier (UUID)
- `name`: Template name (unique)
- `message`: WhatsApp message text
- `category`: Template category
- `variables`: Template variables (JSONB array)
- `media_url`: Optional media attachment (Google Drive link)
- `is_active`: Template status
- `created_at, updated_at`: Audit trail

---

## 28. ACTIVITY_LOGS
**Purpose:** Complete audit trail of all system activities

**Fields:**
- `id`: Unique log identifier (UUID)
- `user_id`: User who performed action
- `action`: Action type (INSERT/UPDATE/DELETE/LOGIN/LOGOUT)
- `action_type`: Action category (create/edit/delete/view/approve/reject)
- `entity_type`: Table name
- `entity_id`: Record ID
- `entity_name`: Human-readable name
- `project_id`: Link to project (optional)
- `old_values`: Before values (JSONB)
- `new_values`: After values (JSONB)
- `changed_fields`: Modified fields (Array)
- `description`: Action description
- `ip_address`: User IP
- `user_agent`: Browser info
- `location`: User location
- `device_info`: Device details (JSONB)
- `session_id`: Session identifier
- `request_id`: Request identifier
- `duration_ms`: Operation duration
- `metadata`: Extra data (JSONB)
- `created_at`: Action timestamp

---

## 29. SYSTEM_LOGS
**Purpose:** System error and event logging

**Fields:**
- `id`: Unique log identifier (UUID)
- `log_level`: Severity (INFO/WARNING/ERROR/CRITICAL)
- `module`: System module
- `message`: Log message
- `error_code`: Error code
- `stack_trace`: Error stack trace
- `context`: Log context (JSONB)
- `created_at`: Log timestamp

---

## 30. PROJECT_DEPENDENCIES
**Purpose:** Track inter-project dependencies

**Fields:**
- `id`: Unique dependency identifier (UUID)
- `project_id`: Dependent project
- `depends_on_project_id`: Required project
- `dependency_type`: Dependency type (finish_to_start/start_to_start)
- `description`: Dependency details
- `created_at`: Creation timestamp

---

## 31. BENEFICIARIES
**Purpose:** Detailed beneficiary tracking with personal and impact data

**Fields:**
- `id`: Unique beneficiary identifier (UUID)
- `beneficiary_code`: Human-readable unique code
- `project_id`: Link to project
- `first_name, last_name, full_name`: Name details
- `father_name, mother_name`: Parent details
- `date_of_birth, age`: Age details
- `gender`: Gender
- `mobile, email`: Contact details
- `address, city, state, pincode`: Location
- `category`: Social category (SC/ST/OBC/General)
- `is_bpl`: Below Poverty Line flag
- `is_disabled`: Disability flag
- `disability_type`: Disability details
- `education_level, school_name, class_grade`: Education details
- `occupation, annual_income`: Economic details
- `family_size, head_of_family`: Family details
- `enrollment_date`: Program join date
- `status`: Beneficiary status (active/completed/dropped/transferred)
- `completion_date`: Program completion date
- `pre_assessment`: Baseline assessment (JSONB)
- `post_assessment`: Post-intervention assessment (JSONB)
- `progress_reports`: Progress tracking (JSONB array)
- `photo_drive_link`: Photo (Google Drive)
- `id_proof_drive_link`: ID document (Google Drive)
- `documents`: All documents (JSONB array of Drive links)
- `notes`: Additional remarks
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by`: Audit trail

---

## 32. VENDORS
**Purpose:** Vendor master database with performance tracking

**Fields:**
- `id`: Unique vendor identifier (UUID)
- `vendor_code`: Human-readable unique code
- `name`: Vendor name
- `company_name`: Legal entity name
- `vendor_type`: Type (Supplier/Contractor/Service Provider)
- `category`: Classification
- `contact_person, email, phone, alternate_phone`: Contact details
- `address, city, state, pincode`: Location
- `gstin, pan, tan, registration_number`: Tax details
- `bank_name, account_number, ifsc_code, branch`: Banking details
- `rating`: Vendor rating (0-5)
- `performance_score`: Performance score
- `total_orders`: Order count
- `total_value`: Total business value
- `is_active`: Vendor status
- `is_verified`: Verification flag
- `is_blacklisted`: Blacklist flag
- `blacklist_reason`: Blacklist reason
- `documents`: Vendor documents (JSONB array of Drive links)
- `notes`: Additional remarks
- `metadata`: Extra data (JSONB)
- `created_at, updated_at, created_by`: Audit trail

---





---
