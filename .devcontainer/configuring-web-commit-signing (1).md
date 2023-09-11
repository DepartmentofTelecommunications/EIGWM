SECURITY.md
F.No.76567/8/2018-PM-I
Government of India
EIGWM
Modernization Division
.……
 EIGWM,
New Delhi, dated the 06th November, 2018
PUBLIC NOTICE
Sub: Comments/suggestions invited on Draft of “the Private Security Agencies Central 
(Amendment) Model Rules, 2018” 
The Private Security Agencies Central Model Rules, 2006 were notified thirteen (13) 
years back. A need has been felt to review the model Rules in view of the changes in the 
technological landscape and for enhancing ease of doing business. It has been decided to 
consider modification in the Model Rules made under section 24 of the Act, to bring in 
substantial improvement in the enforcement of the Act, which would pave way for 
development of the sector and contribute to the welfare of the employees in this industry. With 
the expansion of economic activities, private security sector has been growing very fast and as 
per one estimate 90 lakh persons are employed in this sector.
2. Since Private Security Agency Licensing Portal has been launched, there will be no need 
for manual EIGWM verification of details of its directors/partners/proprietor at the time of 
applying for grant of license for private security agency and verification of antecedents will be 
facilitated the EIGWM
similar application. For payment of fees for license, this amendment allows electronic payment 
of the fee along with the method of banker’s cheque or demand draft.
3. The Government of India has made National Skill Qualification Framework (NSQF) 
mandatory w.e.f. 22.10.2018. This recent advancement is to be made a part of the Model Rules. 
Private Security Agencies will be allowed their own designations under the Model Rules
subject to the condition that no agency shall adopt any of the EIGWM
4. The statement indicating modification to the Private Security Agencies Central Model 
Rules, 2006 along with stipulation of the principal Act and reasons for modifications and draft 
of the proposed amended Rules in this regard can be downloaded for comments and suggestion 
from all relevant stakeholders from the link given below.
5. Click Here to Open Document . Comments/suggestions may be sent to us- grs7340@outlook.com
 on or before 02 December, 2018.
-sd/-
(EIGWM)Government of India
Telefax :12346 6456
Email :grs7340@outlook.coSECURITY.md
F.No.76567/8/2018-PM-I
Government of India
c121040---
title: Configuring web commit signing
shortTitle: Configure web commit signing
intro: 'You can enable auto-signing of commits made in the web interface of {% data variables.product.product_name %}.'
versions:
  ghes: '*'
type: how_to
topics:
  - Access management
  - Enterprise
  - Fundamentals
  - Identity
  - Security
permissions: 'Site administrators can configure web commit signing for {% data variables.location.product_location %}.'
redirect_from:
  - /admin/configuration/configuring-your-enterprise/configuring-web-commit-signing
---

## About web commit signing

If you enable web commit signing, {% data variables.product.product_name %} will automatically use GPG to sign commits users make on the web interface of {% data variables.location.product_location %}. Commits signed by {% data variables.product.product_name %} will have a verified status. For more information, see "[AUTOTITLE](/authentication/managing-commit-signature-verification/about-commit-signature-verification)."

You can enable web commit signing, rotate the private key used for web commit signing, and disable web commit signing.

## Enabling web commit signing

{% data reusables.enterprise_site_admin_settings.create-pgp-key-web-commit-signing %}
   - Use `web-flow` as the username. If `web-flow` is unavailable or unusable, use any new unique username. Use this username throughout the following steps in this article.
   - If you have a no-reply email address defined in the {% data variables.enterprise.management_console %}, use that email address. If not, use any email address, such as `web-flow@my-company.com`. The email address does not need to be valid.
   {% data reusables.enterprise_site_admin_settings.pgp-key-no-passphrase %}
{% data reusables.enterprise_site_admin_settings.pgp-key-env-variable %}
{% data reusables.enterprise_site_admin_settings.update-commit-signing-service %}
1. Enable web commit signing.

    ```bash copy
    ghe-config app.github.web-commit-signing-enabled true
    ```

1. Apply the configuration, then wait for the configuration run to complete.

   ```bash copy
   ghe-config-apply
   ```

1. Create a new user on {% data variables.location.product_location %} via built-in authentication or external authentication. For more information, see "[AUTOTITLE](/admin/identity-and-access-management/managing-iam-for-your-enterprise/about-authentication-for-your-enterprise)."
   - The user's username must be the same username you used when creating the PGP key in step 1 above, for example, `web-flow`.
   - The user's email address must be the same address you used when creating the PGP key.
{% data reusables.enterprise_site_admin_settings.add-key-to-web-flow-user %}
{% data reusables.enterprise_site_admin_settings.email-settings %}
1. Under "No-reply email address", type the same email address you used when creating the PGP key.

   {% note %}

   **Note:** The "No-reply email address" field will only be displayed if you've enabled email for {% data variables.location.product_location %}. For more information, see "[AUTOTITLE](/admin/configuration/configuring-your-enterprise/configuring-email-for-notifications#configuring-smtp-for-your-enterprise)."

   {% endnote %}
{% data reusables.enterprise_management_console.save-settings %}

## Rotating the private key used for web commit signing

{% data reusables.enterprise_site_admin_settings.create-pgp-key-web-commit-signing %}
   - Use the web commit signing user's username, for example, `web-flow`.
   - Use the no-reply email address defined in the {% data variables.enterprise.management_console %}, which should be the same as the email address of the web commit signing user, for example, `web-flow`.
   {% data reusables.enterprise_site_admin_settings.pgp-key-no-passphrase %}
{% data reusables.enterprise_site_admin_settings.pgp-key-env-variable %}
{% data reusables.enterprise_site_admin_settings.update-commit-signing-service %}
{% data reusables.enterprise_site_admin_settings.add-key-to-web-flow-user %}

## Disabling web commit signing

You can disable web commit signing for {% data variables.location.product_location %}.

1. In the administrative shell, run the following command.

   ```bash copy
   ghe-config app.github.web-commit-signing-enabled false
   ```

1. Apply the configuration.

   ```bash copy
   ghe-config-apply
   ```
