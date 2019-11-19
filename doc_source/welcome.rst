.. Copyright 2010-2019 Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

   .. _welcome:

################################
AWS SDK for .NET Developer Guide
################################

The |sdk-net| makes it easier for Windows developers to build .NET applications that tap into the
cost-effective, scalable, and reliable AWS services such as |S3long| (|S3|) and |EC2long| (|EC2|).
The |sdk-net| supports 
.NET Framework 3.5, .NET Framework 4.5, .NET Standard 1.3, .NET Standard 2.0, Portable Class Library, and Xamarin.
You can develop applications with the SDK using Visual Studio 2010 or later.

Unless explicitly stated otherwise,
all information within this guide applies to all of the supported targets.

What's in the SDK
=================

The |sdk-net| includes the following:

* The current version of the |sdk-net|

* All previous major versions of the |sdk-net|

* Sample code that demonstrates how to use the |sdk-net| with several AWS services

To simplify installation, AWS provides the |TFW|, which is a Windows installation package that
includes:

* The |sdk-net|_

* The |TWPlong| (see the |TWP-ug|_)

* The |TVSlong| (see the |TVS-ug|_)

To install the |TFW|,
navigate to the `AWS SDK for .NET <https://aws.amazon.com/sdk-for-net/>`_
select **Download MSI Installer**, save the MSI file, and run it.

As an alternative to installing the |TFW|, you can use NuGet to download individual AWSSDK service
assemblies for a specific application project. For more information, see :ref:`net-dg-nuget`.

.. note:: We recommend using Visual Studio Professional 2010 or later to implement your applications.

.. _about_tools:

About the |TFW| Tools
=====================

|sdk-net|
---------

This document is the developer guide for the |sdk-net|.
The |sdk-net| makes it easier for Windows developers to build .NET applications that tap in to the
cost-effective, scalable, and reliable AWS infrastructure services such as |S3long|, |EC2long|,
|LAMlong|, and more.

AWS Tools for Windows PowerShell and PowerShell Core
----------------------------------------------------

The |TWPlong| and AWS Tools for PowerShell Core are PowerShell 
modules that are built on the functionality exposed by the AWS SDK for .NET. The AWS 
PowerShell Tools enable you to script operations on your AWS resources from the 
PowerShell command line. Although the cmdlets are implemented using the service clients 
and methods from the SDK, the cmdlets provide an idiomatic PowerShell experience for 
specifying parameters and handling results. 

See `AWS Tools for Windows PowerShell <https://aws.amazon.com/powershell>`_ to get started.

|TVSlong|
---------

The |tvs| is a plugin for the Visual Studio IDE that makes it easier for you to develop, debug, and deploy .NET applications
that use Amazon Web Services. The |tvs| provides Visual Studio templates for AWS services and deployment
wizards for web applications and serverless applications. You can use the AWS Explorer to manage |EC2long| instances,
work with |DDBlong| tables, publish messages to |snslong| queues, and more, all within Visual Studio.

You can quickly deploy an existing web application using |tvs|.
See `Deploying Web ApplicationsDeploying Web Applications from Visual Studio <https://docs.aws.amazon.com/sdk-for-net/v3/ndg/web-deploy-vs.html>`_.

See `Setting up the AWS Toolkit for Visual Studio <https://docs.aws.amazon.com/toolkit-for-visual-studio/latest/user-guide/setup.html>`_ to get started.

|TTSlong|
---------

In addition to the tools that the |TFW| installs, you can also install the |TTSlong|.

|TTSlong| (VSTS) adds tasks to easily enable build and release pipelines in VSTS and
Team Foundation Server (TFS) to work with AWS services. You can work with |S3|, |AEBlong|,
|CDlong|, |LAMlong|, |CFNlong|, |SQSlong| (|SQS|), and
|SNSlong| (|SNS|). You can also run commands using the Windows PowerShell
module and the AWS CLI. 

To get started with |TTSlong|, see  `AWS Tools for Microsoft Visual Studio Team Services <https://aws.amazon.com/vsts/>`_.

.. _version_3.5:

What's New in Version 3.5
=========================

This version of the SDK supports only .NET Standard 2.0.
This means you might have to change some of your existing code to use this version.

This version of the SDK supports only asynchronous calls to |AWS| services.
This means that you will have to change any code that uses the old **begin/end** methods.
See
:ref:`net-dg-v35`
for information on adapting V3.0 apps to V3.5.

This version of the SDK contains high-level level abstractions
that make using |COGSYNClong| and |MAlong| easier.
As such, these have been removed from the SDK.
Use |PINlong| instead of |MAlong|; 
use |APSYlong| instead of |COGSYNClong|.

.. _xamarin:

Xamarin
-------

Xamarin apps must target .NET Standard 2.0.
See 
`.NET Standard 2.0 Support in Xamarin.Forms <https://docs.microsoft.com/en-us/xamarin/xamarin-forms/internals/net-standard>`_
and
`.NET implementation support <https://docs.microsoft.com/en-us/dotnet/standard/net-standard#net-implementation-support>`_.

.. _unity:

Unity
-----

Unity apps must target .NET Standard 2.0 or .NET 4.x profiles using Unity 2018.1 or later.
See
`.NET profile support <https://docs.unity3d.com/2020.1/Documentation/Manual/dotnetProfileSupport.html>`_.
In addition, if you are using **IL2CPP** to build,
you must disable code stripping by adding a *link.xml* file.
See
`Referencing the AWS SDK for .NET Standard 2.0 from Unity, Xamarin, or UWP <https://aws.amazon.com/blogs/developer/referencing-the-aws-sdk-for-net-standard-2-0-from-unity-xamarin-or-uwp>`_.

Once you've ported your code to one of the recommend code bases,
your Unity app can now access all of the services offered by the SDK.
Since .NET Standard 2.0 natively supports Unity,
**AWSSDK.Core** no longer has Unity-specific code.

.. _uwp:

Universal Windows Platform (UWP)
--------------------------------

UWP apps must target version 16299 or later.
See
`Choose a UWP version <https://docs.microsoft.com/en-us/windows/uwp/updates-and-versions/choose-a-uwp-version>`_.

.. _phone_silverlight:

Windows Phone, Silverlight
--------------------------

This version of the SDK does not support these platforms as
Microsoft has placed these platforms on an end-of-life path.
See
`Windows 10 Mobile End of Support: FAQ <https://support.microsoft.com/en-us/help/4485197/windows-10-mobile-end-of-support-faq>`_
and
`Silverlight End of Support <https://support.microsoft.com/en-us/help/4511036/silverlight-end-of-support>`_.

.. _legacy:

Legacy Portable Class Libraries (Profile-Based PCLs)
----------------------------------------------------

Retarget these apps to the .NET Standard.
See
`Comparison to Portable Class Libraries <https://docs.microsoft.com/en-us/dotnet/standard/net-standard#comparison-to-portable-class-libraries>`_.





.. _guidemap:

How to Use This Guide
=====================

The *AWS SDK for .NET Developer Guide* describes how to implement applications for AWS using the
|sdk-net|, and includes the following:

:ref:`net-dg-setup`
    How to install and configure the |sdk-net|. If you have not used the |sdk-net| before or are
    having trouble with its configuration, you should start here.

:ref:`net-dg-programming-techniques`
    The basics of how to implement applications with the |sdk-net| that applies to all AWS services.
    This section also includes information about how to migrate code to the latest version of the
    |sdk-net|, and describes the differences between the last version and this one.

:ref:`tutorials-examples`
    A set of tutorials, walkthroughs, and examples showing how to use the |sdk-net| to create
    applications for particular AWS services.
    You can browse the |sdk-net| examples in the
    `AWS Code Sample Catalog <https://docs.aws.amazon.com/code-samples/latest/catalog/code-catalog-dotnet.html>`_.

:ref:`net-dg-additional-resources`
    More resources outside of this guide that provide valuable information about AWS and the
    |sdk-net|.
    If you are unfamiliar with AWS services,
    see the `Overview of Amazon Web Services <https://docs.aws.amazon.com/whitepapers/latest/aws-overview/introduction.html>`_.

A related document, |sdk-net-api|_, provides a detailed description
of each namespace and class.


.. _supported-services:

Supported Services and Revision History
=======================================

The |sdk-net| supports most AWS infrastructure products, and more services are added frequently. For
a list of the AWS services supported by the SDK, see the `SDK README file
<https://github.com/aws/aws-sdk-net/blob/master/README.md>`_.

To see what changed in a given release, see the `SDK change log
<https://github.com/aws/aws-sdk-net/blob/master/SDK.CHANGELOG.md>`_.
