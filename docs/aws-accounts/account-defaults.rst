.. _account_defaults:

================
Account defaults
================

For all AWS accounts managed by Rackspace, whether created through the
`Rackspace Technology Customer Portal <https://manage.rackspace.com/aws>`_
or created directly with AWS and transferred to Rackspace, we automatically
apply the following default settings to the account based on best practices we
developed in cooperation with AWS. You should not change or disable
any of these default settings because they are critical to our delivery of
Fanatical Support.

**AWS Identity and Access Management (IAM)**:

  * Set up an IAM role named **Rackspace** for ongoing access to the account.
    See :ref:`aws_iam` for additional details.
  * Set the IAM account password policy for all passwords. Passwords have
    the following requirements:

    * Are at least 12 characters in length.
    * Contain at least one uppercase character.
    * Contain at least one lowercase character.
    * Contain at least one number.
    * Contain at least one symbol.
    * Are not one of the previous 24 passwords used.

  * Create an IAM role named **AWSConfig** for the AWS Config service to use.
  * Create an IAM role named **CloudHealth-Role** to enable us to provide you
    with :ref:`CloudHealth <cloudhealth>`.

    * Tampering or removing this role could cause overbilling.

  * Create an IAM role named **RackspaceDefaultEC2Role** with an attached
    IAM policy named **RackspaceDefaultEC2Policy** that you can attach to
    EC2 instances to provide access to
    `AWS Systems Manager <https://aws.amazon.com/systems-manager/>`_ and the
    `CloudWatch EC2 Agent <https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html>`_.
  * Create an IAM role named **EC2ActionsAccess** for CloudWatch alarms to use
    to trigger actions on instances.

**AWS Simple Storage Service (S3)**:

  * Create a bucket named **<account_uuid>-logs** in the **US West 2** (Oregon)
    region with the following settings:

    * Enable versioning and apply an S3 bucket lifecycle policy to the
      **<account_uuid>-logs** bucket that expires files after 365 days and
      permanently removes deleted files after 90 days.
    * Set an S3 bucket policy on the **<account_uuid>-logs** bucket to allow
      write access from CloudTrail.

  * Create a bucket named **<account_uuid>-ssmoutput** in the **US West 2**
    (Oregon) region with the following settings:

    * Apply an S3 bucket lifecycle policy to the **<account_uuid>-ssmoutput**
      bucket that deletes files after 60 days.

**AWS CloudTrail**:

  * Configure `AWS CloudTrail <https://aws.amazon.com/cloudtrail>`_ in each
    AWS region to log to the S3 bucket named **<account_uuid>-logs**.
  * Configure an SNS topic named **rackspace-cloudtrail** in each region and
    subscribe it to a region-specific Shared Management Services SQS queue
    for use by the :ref:`Rackspace Logbook <logbook>` service.

**AWS Config**:

  * Configure `AWS Config <https://aws.amazon.com/config/>`_ in each AWS
    region to log to the S3 bucket named "<account_uuid>-logs"
  * Configure an SNS topic named "rackspace-awsconfig" in each region and
    subscribe it to a region-specific Shared Management Services SQS queue
    for use by Rackspace tooling

**AWS Simple Notification Service (SNS)**:

  * Create SNS topics named **rackspace-support**, **rackspace-support-standard**,
    **rackspace-support-urgent**, **rackspace-support-emergency** in each
    region and subscribe it to a region-specific Shared Management Services
    SQS queue for use by our :ref:`Rackspace Watchman <watchman>` service.
