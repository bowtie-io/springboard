# What is &#8904;Bowtie.io?

&#8904; BowTie is a developer-centric toolkit for turning software into
a business. It is designed to launch MVPs (minimum viable products). The BowTie
platform provides smart styling, themes, business logic, communication utilities
and marketing tools to your application. An application wrapped with BowTie
becomes a product that functions in the real world.

# Platform

## Backend

A [Backend Application](#platform-backend-application) - while optional -
provides logic for your application domain. It's the core of your business, what
differentiates your system from all others and what provides distinguishable
market value to your product.

A [Backend Application](#platform-backend-application) is an application built
with your preferred web application development platform. It may be a single document,
a single page Javascript application, or a complex Rails application.

In a brewery ranking application the index of breweries, their rankings, and the
interface to change or update a brewery or a ranking are provided by the Backend
Application.

## Frontend

Your application's [Frontend](#platform-frontend) is logic required for Project
release, but not part of the application domain provided by the
[Backend Application](#platform-backend-application).

In the brewery ranking application, the methods to authenticate and monetize
the index of breweries and their rankings are provided by the
[Frontend](#platform-frontend) application.

## Project

A BowTie [Project](#platform-project) consists of a reference to a
[Backend Application](#platform-backend-application) wrapped with the BowTie
*Frontend* and platform tools.

If A [Project](#platform-project) may be built with the BowTie platform entirely,
depending on the [Backend Application's](#platform-backend-application)
complexity (static content-based sites and single page Javascript applications function
well without a traditional [Backend Application](#platform-backend-application).

A [Backend Application](#platform-backend-application) may be built with your favorite
web application development platform. BowTie is capable of turning a single-user
web application into a multi-user web application.  Create a BowTie
[Project](#platform-project) to manage styling and UI.


## Project Site

Your *Project Site* is available at https://projectname-environment.bowtied.io/, or on
your *Custom Domain*.

Domain Type    | Project Name | Environment | URL
---            | ---          | ---         | ---
Bowtied Domain | example      | development | https://example-development.bowtied.io/
Bowtied Domain | example      | staging     | https://example-staging.bowtied.io/
Bowtied Domain | example      | production  | https://example.bowtied.io/
Custom Domain  | example.com  | development | https://development.example.com/
Custom Domain  | example.com  | staging     | https://staging.example.com/
Custom Domain  | example.com  | production  | https://example.com/

## Domains

*Bowtied Domains* are for *Project Sites* hosted on the https://bowtied.io domain. They are available at
https://projectname-environment.bowtied.io/.

*Custom Domains* are provided and may be purchased through the BowTie platform. BowTie supports purchasing
domains for the 'com', 'net', 'biz', 'org', 'info', and 'mobi' TLDs.

## SSL/TLS

All *Project Sites* on BowTie are configured to respond over 128 bit TLS with HSTS.

*Bowtied Domains* use a wildcard SSL certificate configured for https://*.bowtied.io/.

*Custom Domains* purchased with BowTie include a certificate for the production *Project Site*,
and use a self-signed certificate for the development and staging *Project Sites*.

Contact us to purchase additional certificates for the development and staging *Project Sites* for *Custom Domains*.

## Dashboard

Project statistics and management interfaces are provided by an easily
accessible UI refered to as the *Project Dashboard*. A powerful but simple
*Website Editor* on the *Project Dashboard* provides the ability to quickly
adjust the most important content on your site. The *Project Dashboard* is
accessed by logging in to the *BowTie Dashboard* and selecting your *Project*.

## Repositories

The *Project Repository* is a git repository containing a *Frontend Theme*,
*Legal Documentation*, and *Policy Files* for managing access to your
application's resources. You can manage most of your *Project* configuration by
editing content within this repository. A simple `git push` to the BowTie remote
from your local repository will trigger BowTie's systems to update your
application.

Use your development system's `git` installation to perform the clone operation:

```bash
$ git clone CLONEURL
```

where `CLONEURL` should be replaced with the Clone URL from the *Project
Dashboard*.

A `README.md` file in the cloned source will help you get started with
development on your local system.

### Keys

Access to a *Project Repository* is restricted based on SSH keys. A *Key* is configured
for your account, and any *Project* associated with your account can be accessed with the
same *Key*.

Use an existing SSH key, or generate a new `ssh key` pair. Github has a great
[reference](https://help.github.com/articles/generating-ssh-keys/) if you're new
to this process. _Keys must be at least 512 bits._

Once a valid *Key* has been added to your account, you can clone and push commits to
your *Project Repositories*.

## Environments

The *Project Repository* contains three branches, which correlate to different
environments your application can run under. The `master` branch is the
*Production Environment*, the `staging` branch is the *Staging Environment*, and
the `development` branch is the *Development Environment*.

Changes in the *Project Dashboard* will affect the `development`
branch. From your *Project Repository* checkout, you can promote these changes
by merging or rebasing into the desired environment.

Unless otherwise stated this documentation assumes you cloned your repository directly
from the BowTie clone url without additional options, and that 'origin' points to the
BowTie repository servers.

Pushing content to 'origin' will create a new *Release* and promote the changes
to your live *Project Site*.

To promote from `development` to `staging`:

```bash
$ git checkout staging
$ git merge development
$ git push origin staging
```

To promote from `staging` to production (`master`):

```bash
$ git checkout master
$ git merge staging
$ git push origin master
```

Depending on your development workflow, you may encounter merge conflicts that
should be resolved using your preferred git resolution pattern. Please see the
git documentation for more information on resolving conflicts.

# Tools

## Prospects

Prospective *Project Users* are individuals on your *Project's* mailing list.
Your *Project* includes a `bowtie.js` file from the BowTie server that
enables methods you can use to add users to this mailing list.

```javascript
bowtie.prospects.register(email)
```

This returns a jQuery promise you can use for handling errors and callbacks:

```javascript
bowtie.prospects.register('prospect@example.com')
  .then(function(){
    alert("Successfully signed up to mailing list!");
  })
  .fail(function(){
    alert("Failed to sign up to the mailing list!");
  });
```

The 'email-signup' Section from the *Project Splash Page* section provides
a functioning integration you can use without additional code.

## Users

Projects wrapped with BowTie are provided a fully managed Devise-based User
authentication system. This includes registration forms, sign in
forms, password reset functionality and more. A Project concerned with
implementing a User resource can determine a unique User identifier from the
`X-Bowtie-User-Id` header passed to the Backend Application, or on the client
with BowTie's javascript `bowtie.user.X` interfaces.

User data is also available to Policy objects, allowing Projects to restrict
access to resources based on User information.

A [User](#tools-users) is an individual with a registration to your
[Project](#platform-project). Your [Project Site](#platform-project-site)
contains the following preconfigured endpoints you can use to adjust your
Project's Account User Experience.

[User](#tools-users) records are not shared amongst your *Projects*. A *User* will have to
sign up for each *Project* individually.

### Interfaces

#### /users/sign_up

User and Subscription registration pathway. Provides a prospective *User* the
ability to register to your Project.

#### /users/sign_in

Sign in for existing *Project Users*

#### /users/sign_out

Signs out a *Project User* with a current session.

Has no affect on visitors with no session. Redirects back to sign_in page.

#### /users/password/new

Allow a visitor to begin the password reset procedure.

#### /users/password/edit

Allow a *Project User* with a session to change their password.

#### /users/confirmation/new

An unconfirmed *Project User* resends the confirmation email.

#### /users/unlock/new

A *Project User* begins the process of unlocking a locked account.

### Backend Request Headers

HTTP Headers are added to *Project Backend* requests when the Backend is
enabled. These headers are not available until a *Project User* session exists:

#### X-Bowtie-User-Id

A unique value that represents the user that's logged in. Use this value for
storing data related to the user, since it will not change with an updated email
address.

#### X-Bowtie-User-Name

Name provided by User during registration. Not provided if not collected.

#### X-Bowtie-User-Email

Email provided by the User during registration.

#### X-Bowtie-User-Plan

Stripe Plan ID if User is subscribed to a plan. Blank string if *Project User* is not subscribed
to a plan.

### Javascript Methods

Methods available to the browser when `bowtie.js` is included from the BowTie
servers.

#### bowtie.user.info()

Returns an object with information about the current  *Project User*

```javascript
  bowtie.user.info(function(user){
    if(!user){
      // There is no user signed in

    }else{
      // Name provided by User during registration. `undefined` if not collected
      console.log(user.name);

      // Email provided by User during registration.
      console.log(user.email);

      // Stripe Plan ID if User subscribed to a Plan. `false` if User is not subscribed to a plan.
      console.log(user.plan);
    }
  });
```

## Subscriptions

_Pending next major release_

Your Project may require Users to Subscribe to a Plan for periodic charges to
a Credit Card they've associated with their User account. BowTie support for
subscriptions allows you to configure Stripe Plans and "track" them for use by
your Project.

After connecting your Project to Stripe via the 'Stripe Connect' interface, you
can select to 'Track' a Stripe Plan. Tracked Plans may be selected by *Project
Users* during a new user Registration and updated at the Project
"/users/subscription" endpoint.

An untracked plan will not be eligible for purchase with the *BowTie Frontend*.

Plans currently in use by a Project User cannot be untracked.

The `bowtie.user.info()` method will return an object containing a `plan`
attribute containing the Stripe Plan ID of the Tracked Plan the User is
registered with.

The 'X-Bowtie-User-Plan' section will provide the Stripe Plan ID of the Tracked
Plan a User is registered with to the [Backend Application](#platform-backend-application).

## Payments

_Pending next major release_

## Policies

Resource access, which includes any request to your *Project Frontend* and your
*Project Backend* is filtered by Access Control Policies contained in the
`policies` directory of your *Project Frontend Source*.

A *Policy* contains a declaration of the resource to be protected and a `read`
and `write` method that receive information about the request. By returning
`true` or `false` you can restrict access to the information at the protected
resource path.

```javascript
// ./policies/dashboard.js
/*
  Prevent access to /dashboard* for all users without a subscription plan.
*/
{
  protects: '/dashboard',

  read: function(request){
    if(!request.plan){
      return false;
    }
  },

  write: function(request){
    if(!request.plan){
      return false;
    }
  }
}
```

The `request` object given to the `read` and `write` methods has the following
structure:

```json
  // <policy:request>
  {
    headers: <policy:headers>,
    path: <policy:path>,
    user: <policy:user>,
    plan: <policy:plan>,
    subscription: <policy:subscription>
  }

  // <policy:path>
  /dashboard/overview

  // <policy:headers>
  {
    "accept": "*/*",
    "accept-encoding": "gzip, deflate, sdch",
    ...
  }

  // <policy:user>
  {
    "name": "Sue Smith",
    "email": "user@example.com"
  }

  // <policy:plan>
  "stripe_plan_id"
```

## Email Forwarding

Email to any address on your domain is forwarded to your Account email. For
instance, if you registered `example.com`, then any address for `example.com` (`someone@example.com`)
will forward to the email configured on your *Account Dashboard*

## Status Pages

_Pending next major release_

Since BowTie hands manages requests to your Project's [Backend Application](#platform-backend-application), it is aware of server errors and latency issues encountered by *Project
Users*. Bowtie provides a `/status` interface for your Project where you can
direct traffic for an overview of your application health.

As the *Project Owner* you may opt in for status alerts with your mobile device
or via email.

## DNS

The `dns.json` file in your *Project Repository* working directory contains
subdomain DNS entries for your Project's zone.

Adding or removing an entry from this file changes the DNS records for the
*Project Environment* on the related branch.

### Records

`DNS records` should all be in a records attribute in their own object.

```json { "records": [ {}, {} ] } ```

**Record Types:**

##### A

The `Address Record` maps an hostname to an IP address.

```json { "name": ".", "type": "A", "ipv4": "{{project.servers.web}}" } ```

##### CNAME

The `Canonical Name Record` maps one hostname to another.

```json { "name": "bar.example.com.", "type": "CNAME", "target":
"{{project.servers.web}}" } ```

##### MX

The `Mail Exchange Record` maps a domain to a list of mail servers for the
domain.

```json { "name": ".", "type": "MX", "priority": "10", "target":
"{{project.servers.mail1}}" } ```

##### SRV

The `Service Locator Record` is a generalized location record, it can be used in
place of more specific records like `MX`.

```json { "name": "service", "type": "SRV", "data": "target", "priority": 0,
"port": 9012, "weight": "2" } ```


##### TXT

The `Text Record` can hold arbitrary data, it is often used in domain identity
processes.

```json { "name": "text", "ttl": 400, "value": "value" } ```

# Guide

## Configure a Project

### Name

### Theme

### Legal

## Build a Backend Application

### Application Logic

### Subscription Lockdown

## Launch

### Deployment

### Analytics

### Maintenance

# Releases

All Projects are displayed in a single UI, accesible via the &#8904; BowTie
[login](https://bowtie.io/owners/sign_in/). Feature sets for each release are
included below. The current release is: **11/15/2014 MVP Release**

## 11/15/2014 MVP Release

This is the first semi-public release of the &#8904; BowTie platform. Access
by invitation only.

![release snapshot 11-15-14](/documentation/images/bowtie-11-15-14.png)

* Dashboard Track visits, actions, payments and sign ups Website Editor Elegant
* single page [bootstrap](http://getbootstrap.com/) website template with
* WYSIWYG builder Email Tools Capture emails on pre-built landing page, export
* to csv User Management User roles, pipelines, customizable fields and roles
* Payments Simple connection to Stripe for payments and subscriptions Legal
* Tools
  - One-click Terms of Service generator
* General Features
  - Project Repositories
    - &#8904; BowTie creates Development/Staging/Master branches with single
      command promotion
  - Always SSL hosted domains at https://bowtied.io
  - Email Forwarding
    - Domain level email is automatically forwarded to a specified address
  - Maintenance Mode
    - Preconfigured maintenance site that deploys with the flip of a switch

# Dashboard Tour

&#8904; BowTie is designed to be intuitive but a tour never hurts. This section
will walk through all features of the current user interface so everything is
clear.

## Registration

Welcome to &#8904; BowTie!  Each time you sign in you will enter the platform at
the Dashboard.  The first thing you will notice is a large orange banner to help
you get started.  This banner will continue to guide you until you make a commit
and really dig in.  Follow the directions on the banner to grab your Clone URL
(located right below the banner).  Next make a commit and push.  You are in
business.  You will also notice that your website is already live (awesome!) but
we will get to that in a minute.  At the top left of the platform is a drop down
for all your projects.  What is a project you say?  In the &#8904; BowTie world,
  a project is any application you host with us.  You can host as many as you
  like and move between then using this drop down menu.  Go ahead...test a ton
  of different ideas.  You will also see Account Settings and Logout, but we
  will get to these later.

## Project Dashboard

Each time you sign into &#8904; BowTie you will start in the dashboard.  This is
the nerve center of &#8904; BowTie and your new best friend.  Here you will find
all the analytics you want to track your application and site.

* **Vistors** - how many unique visitors see your new site **Subscribers**
* - track how many people signup on your site **Users** - the number of users
* your application currently has **Actions** - tracks all the interactions with
* your application from creation of user accounts and beyond **Pipeline** - here
* you can see what kind of conversions you have for any of the various plans you
* set up on &#8904; BowTie for your application **Preview** - from the dashboard
* you can preview your fancy new website in Dev, Staging, and Master (described
* above).  These will take you to previews of your site so you can see how
* awesome it is.

## Website

When you signup with &#8904; BowTie you get a live site immediately.  It is
built with Bootstrap and is ready for you to start customizing it.  At the top
of this page you will see the link to your site.  Go ahead, give it a look.
Below this there are two main components to the Website section - Site Settings
and Site Content.

### Site Settings

Everything in the Site Settings section applies to all of your project (the site,
error pages, the maintenance page, etc).

  - **Page Info and Meta Data** - here you can give your page a title and any
    meta keywords you think are best.  These keywords will help tell search
    engines what your site and application are all about.  They won't appear
    anywhere on your site but will be "behind the scenes."
  - **Webfonts and Icons** - pick any font to start giving your site a custom
    look.  Alternatively try one of the pre-configured fonts by just checking
    the box.  My favorite is FontAwesome.
  - **Analytics** - if you are like us, you can never have enough data.  In
    addition to the &#8904; BowTie Dashboard, you connect to Google Analytics to
    see additional site traffic data.
  - **Favicon/Bookmark Icons** - upload your logo or image that you would like
    to use.  The favicon is the nifty little image you see in bookmarks and next
    to the title of a site up in the tab of your browser.  Kind of like our
    awesome &#8904; BowTie icon!

## Site Content

This section has two parts - the input section and the preview section.

- **Input** - The input section allows you to customize each part of your page.
  The template page you are starting with is broken up into panels much like the
  main [&#8904; BowTie site](http://bowtie.io/).  Each part of the input section
  is roughly broken up the same way, allowing you to control the different
  pieces of your site.  Each part can be removed or more panels can be added.
  It is up to you!
  - Intro/Heading lets you add a hero image and titles to the first panel of
    your page.
  - Navigation allows you to customize how your users will navigate the
    different parts of your site.
  - Email Form controls how you collect information from your users and what
    information you collect.  You can even add a countdown timer to let your
    users know when you plan to launch!
  - Features give you an intuitive panel to talk about your application, add
    some pictures, and make a call to action to get your users excited.
  - About/Team lets you showcase you and your team.  Go ahead, put a picture of
    that pretty mug up there.
  - Footer gives you a place for all your social media links and icons.
  - Section is a generic panel or section of your website just in case you have
    more to share.

- **Preview**
  - The Preview section lets you see all the changes you are making as you make
    them.  As you are customizing your site you can save your progress.
  - When you are done making changes and like what you have built you can
    promote the site up to the next staging environment.

## Users

As with any application, you need to be able to track and measure your user
base.  Who has signed up, contact information, and more.  There are two main
sections under Users; User List and Add Users.
* User List
- Track all the important information about your users.  See users Identities,
  Registration information, date of last login (see how active they are), and
  the Last Action they had with your application.
* Add Users
- Manually add users to your application.  Fill out all the needed information
  for a new user and click on Create User.  They will be added to the User List
    and now be active on your application.

## Payments

&#8904; BowTie is preconfigured with Stripe so you have industry leading payment
functionality and security.  You can also configure your own payment solution
though we are not sure why you would ever want to.
* Add New Connection.  Click on the __Connect to Stripe__ button to setup your
* Stripe account.  Follow their directions to complete the form, add your
* banking information, and activate the account.  Stripe Connection.  This will
* indicate whether you are connected or not with Stripe.  Once you have
* successfully set up your account, this will turn green.  The main part of the
* page will track all transactions and allow you to monitor your account.

## Legal

&#8904; BowTie is all about getting you up and into your customer's hands
quickly.  To assist we offer templates for Terms of Service (TOS).  Required for
all sites, this is the document that outlines the legal responsibility of you
and your users.  These templates are just meant to get you up and running.
Don't forget that the responsibility is yours to make sure these accurately
reflect your business.
* Select the general type of TOS that most closely fits your application.  You
* can deploy the TOS to whichever of your staging environments you would like.

## Settings (Project Settings)

The &#8904; BowTie Project Settings pages allows you to manage all aspects of
your project.
* All of your different environments are there as is your Git Clone URL.  Click
* any of the environment View buttons to see your site in that stage.
* __Maintenance Mode__ let's you suspend access to your site and application.
* It replaces your site with a splash page saying you down for maintenance and
* will be back up soon.  A green indicator will confirm that Maintenance Mode is
* either on or off.  The Project Settings page also contains Domain and Email
* Forwarding instructions discussed above.  You can delete your project with the
* __Delete Project__ button.  This will remove all access to any project data,
* users and user information, and domains.  Maintenance Mode is a non-permanent
* option to also pull down your site and application.  If you aren't sure which
* is best, [contact us](https://beta.bowtie.io/feedback_messages/new).

## Top Menu Controls

The Top Menu is the banner running along the top of the &#8904; BowTie platform.
Here you will find key controls for managing projects at the project level and
controls for managing your overall account with &#8904; BowTie.
* __Project Dropdown__.  This allows you to switch between all your existing
* projects.  No loging out and back in to another account.  Just select and go.
* Create a new project button (the __plus sign__).  If you are like us then you
* will want to launch _many_ projects.  This button allows you to add another
* project to your account so you can spin up another awesome application.
* Clicking on the __plus sign__ will take you to the Create a New Project page.
  - Seach for a domain for your new project.  &#8904; BowTie will automatically
    check the availability of the domain name.
  - See any cost impact to your account related to your existing and new
    project.
  - If you bought your own domain (BYOD) elsewhere, that works too.  Just follow
    the directions above on configuring your CNAME record to point towards your
    &#8904; BowTie account.
* Loging out.  You guessed it.  The little __X__ in the top right corner will
* log you out of the &#8904; BowTie platform.

The Account setting page contains many features useful for managing your access
to &#8904; BowTie.
* __Account__.  Change your email and password as desired.  Additionally you can
* cancel your account here.  If you cancel your account you will lose access to
* your projects as they are set up on &#8904; BowTie, data, user information,
* domains, and files.  If you are having trouble and don't know just how to
* proceed, [contact us](mailto:info@bowtie.io)...we love to help!  __Keys__.
* Add a new SSH key to your project and give it a title.  If you need any help
* in generating a new SSH key, we recommend following Github's [Generating SSH
* Keys](https://help.github.com/articles/generating-ssh-keys/) guide.  Then just
* associate that key with your &#8904; BowTie account and off you go!
* __Billing__.  Manage how your pay for access to &#8904; BowTie.  See details
* about your account and click on __Update Card__ to provide a new or different
* credit card.  __Feedback__.  We love feedback and want to hear what you think.
* Fill out any comments or suggestions you have and let us know.
