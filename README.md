**Component Structure**

The contact form was built using Vue.js 3 with two reusable components:

<contact-form>

Contains the form fields (name, email, message).

Uses v-model for two-way binding.

Props allow customising placeholder text and button labels.

Emits a submitted event when the form passes validation.

<modal-confirm>

Receives the submitted details as props.

Displays them inside a styled modal window.

Emits a close event when the user clicks Close or the backdrop.

The root Vue app (#app) manages state for the modal and passes data between components.


**Validation & Modal Interaction**

Validation Rules:

Name: required, letters/spaces/apostrophes/hyphens only.

Email: required, must match standard email format.

Message: required, at least 10 characters.

Real-time Errors:
Errors are shown under each field using v-if and computed properties, updating instantly as the user types.

Submit Button:
Disabled until all fields are valid (:disabled="!isValid").

Modal Flow:
On valid submission, the form emits the data to the parent app, which opens <modal-confirm>.
The modal can be closed by clicking Close, clicking outside the modal card, or pressing Esc.


**Testing Notes**

Tested in Chrome, Firefox, and Edge using the Vue CDN build.

Checked responsiveness on mobile and desktop layouts.

Verified:

Error messages show/clear instantly.

Submit button only enables when all inputs are valid.

Submitted data correctly appears in the modal.

Modal closes reliably with all three methods.


**Challenges & Resolutions**

Validation logic duplication: At first I repeated code in the template. I resolved this by moving rules into computed properties, which keeps the template clean and updates automatically.

Modal communication: Needed to decide whether the modal should handle its own state. I chose to let the parent app control visibility while the modal only emits close. This separation made the code more reusable.

Accessibility: Ensuring the modal works for all users was tricky. I added aria-modal, role="dialog", and linked the title with aria-labelled by for screen reader support.

Styling consistency: To match the portfolio’s design, I reused existing classes (btn-primary, form-field, error-text) instead of inventing new ones.
