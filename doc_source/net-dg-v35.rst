.. Copyright 2010-2019 Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _net-dg-v35:

##########################
Updating Your Code to V3.5
##########################

This topic describes how to update your existing code to the 3.5 version of the |sdk-net|.

See :ref:`version_3.5` for information about the new 3.5 features
and the changes you might have to make to your app to support .NET Standard 2.0.

.. _async_ops:

Making Asynchronous Calls to |AWS| Services
===========================================

You must use asynchronous methods in this version of the SDK.
For example, here is some 3.0 code to list the URLs of your |SQS| queues.

.. code-block:: c#

   AmazonSQSClient client = new AmazonSQSClient();

   ListQueuesResponse response = client.ListQueues(new ListQueuesRequest());
   
   foreach (var queueUrl in response.QueueUrls)
   {
       Console.WriteLine(queueUrl);
   }

Use
:sdk-net-api:`ListQueuesAsync <SQS/MSQSListQueuesAsyncStringCancellationToken>`
instead:

.. code-block:: c#

   static async Task<ListQueuesResponse> MyListQueuesAsync()
   {
       AmazonSQSClient sqsClient = new AmazonSQSClient();
       ListQueuesResponse response = await sqsClient.ListQueuesAsync("");
       return response;
   }
   // In main:
   Task<ListQueuesResponse> response = MyListQueuesAsync();

   foreach (var q in response.Result.QueueUrls)
   {
       Console.WriteLine(q);
   }
