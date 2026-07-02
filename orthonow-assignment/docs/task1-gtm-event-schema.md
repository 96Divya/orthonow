# Task 1 – GTM Event Schema

## Event Tracking Schema

| Event Name | Trigger Type | Key Parameters | GA4 Report / Audience |
|------------|--------------|----------------|------------------------|
| booking_step_complete | Custom Event (dataLayer) | step_number, clinic_location, specialty | Funnel Exploration |
| booking_completed | Custom Event | booking_id, clinic_location, specialty | Conversions |
| consultation_form_submitted | Form Submit | patient_name, phone_number, source | Conversions |
| click_call_now | Link Click | page_location, phone_number, device_type | Engagement |
| whatsapp_click | Link Click | page_location, campaign_name, device_type | Engagement |
| patient_guide_download | Form Submit + PDF Download | patient_name, phone_number, guide_name | Lead Generation |
| clinic_page_view | Page View | clinic_name, city, specialty | Pages & Screens |
| blog_scroll_25 | Scroll Trigger | article_title, scroll_depth, category | Content Engagement |
| blog_scroll_50 | Scroll Trigger | article_title, scroll_depth, category | Content Engagement |
| blog_scroll_75 | Scroll Trigger | article_title, scroll_depth, category | Engaged Audience |
| blog_scroll_100 | Scroll Trigger | article_title, scroll_depth, category | Completed Reads |

---

## Booking Funnel Tracking

The appointment booking process consists of three steps:

1. Select Clinic Location and Specialty
2. Enter Patient Details (Name, Phone, Preferred Date)
3. Confirm Booking

A custom `dataLayer.push()` is triggered by the front-end developer whenever a user successfully completes each step. Google Tag Manager listens for these events and forwards them to GA4.

This enables funnel analysis in GA4 to identify where users abandon the booking process.

### Step 1

```json
{
  "event": "booking_step_complete",
  "step_number": 1,
  "step_name": "location_specialty_selected",
  "clinic_location": "Indiranagar",
  "specialty": "Knee Pain"
}
```

### Step 2

```json
{
  "event": "booking_step_complete",
  "step_number": 2,
  "step_name": "patient_details_entered",
  "patient_name": "Rahul Sharma",
  "phone_provided": true,
  "preferred_date": "2026-07-05"
}
```

### Step 3

```json
{
  "event": "booking_completed",
  "step_number": 3,
  "step_name": "booking_confirmed",
  "booking_status": "confirmed",
  "clinic_location": "Indiranagar",
  "specialty": "Knee Pain"
}
```
---

## GA4 Funnel Exploration

The funnel in GA4 will be configured using the following steps:

1. booking_step_complete (Step 1 - Location & Specialty Selected)
2. booking_step_complete (Step 2 - Patient Details Entered)
3. booking_completed (Step 3 - Booking Confirmed)

---

## GA4 Funnel Exploration

The funnel in GA4 will be configured using the following steps:

1. booking_step_complete (Step 1 - Location & Specialty Selected)
2. booking_step_complete (Step 2 - Patient Details Entered)
3. booking_completed (Step 3 - Booking Confirmed)

By tracking each step separately, GA4 Funnel Exploration can identify the percentage of users who drop off at each stage. This helps optimize the booking experience by identifying friction points in the user journey.

---

## Google Ads Conversion

### Conversion to Import

**consultation_form_submitted**

### Reason

The `consultation_form_submitted`
 event represents a successful consultation booking and is the strongest indicator of a qualified lead. Importing this event into Google Ads allows Smart Bidding strategies (such as Maximize Conversions or Target CPA) to optimize campaigns toward users who complete the full booking process instead of those who only begin it.