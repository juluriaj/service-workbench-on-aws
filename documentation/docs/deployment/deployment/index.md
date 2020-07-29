---
id: index
title: Deploying Galileo
sidebar_label: Deploying Galileo
---

Run main deployment script
--------------------------

-   Run `scripts/environment-deploy.sh <stage>`

-   It takes 15-20 minutes

-   After the deployment has successfully finished, take a note of its
    CloudFront URL, and the root password.

    > -   This information can be retrieved later by running
    >     `scripts/get-info.sh <stage>`

-   You can now log in to your Galileo deployment using the link above
    and user **root**. The root user will be used only to create
    administrative users which is covered in [Post Deployment](/deployment/post_deployment/index)

Deploy the machine-images SDC (optional)
----------------------------------------

The machine-images SDC provides the ability to launch EC2 images from
within Galileo. The default Galileo installation currently provides
Sagemaker, EMR, and Linux and Windows EC2 as workspace options. The EC2
options will not be available unless you run this step.

-   Follow the steps outlined in
    `main/solution/machine-images/README.md`

    > -   Install Packer (<https://www.packer.io/>). Packer is used to
    >     create a custom AMI which is then pushed to the Galileo
    >     deployment.
    >
    >     > -   Fetch the package with curl or wget, unzip it and copy
    >     >     it to `/usr/local/bin`
    >
    > -   Change directory to `/main/solution/machine-images`
    >
    > -   run `pnpx sls build-image -s <mystage>`
    >
    > -   This will take 15 minutes

-   For examples of how to build a custom AMI, see:

    > -   `config/infra/packer-ec2-<platform>-workspace.json`
    > -   `config/infra/provisioners/provision-hail.sh`

Enable Active Directory Authentication (optional)
-------------------------------------------------

-   Get the relying party information for AD integration (User Pool ID,
    Relying Party ID, User Pool Signing Cert etc)

-   Run the script `scripts/get-relying-party.sh`

    > -   Supply the output of this script to your Active Directory
    >     administrator
    
    See more on adding 
    - [an IDentityProvider](/deployment/configuration/auth/configuring_idp)
    - [Auth0](/deployment/configuration/auth/configuring_auth0)