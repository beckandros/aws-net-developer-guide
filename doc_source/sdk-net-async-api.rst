.. Copyright 2010-2019 Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _sdk-net-async-api:

####################################
|AWSlong| Asynchronous APIs for .NET
####################################

.. _async-api-45:

Asynchronous API for .NET Framework 4.5, Windows Store, and |WP|
================================================================

The |sdk-net| uses the new task-based asynchronous pattern for .NET Framework version 4.5, Windows
Store, and |WP|. You can use the :code:`async` and :code:`await` keywords to perform and manage
asynchronous operations for all AWS products without blocking.

To learn more about the task-based asynchronous pattern, see 
`Task-based Asynchronous Pattern (TAP) <http://msdn.microsoft.com/en-us/library/hh873175(v=vs.110).aspx>`_ 
on MSDN.


.. _async-api-35:

Asynchronous API for .NET Framework 3.5
=======================================

The |sdk-net| supports asynchronous (async) versions of most of the method calls exposed by the .NET
client classes. The async methods enable you to call AWS services without having your code block on
the response from the service. For example, you can make a request to write data to |S3| or |DDB|
and then have your code continue to do other work while AWS processes the requests.

.. _sdk-net-async-request-syntax:

Syntax of Async Request Methods
-------------------------------

There are two phases to making an asynchronous request to an AWS service. The first is to call the
:code:`Begin` method for the request. This method initiates the asynchronous operation. The
corresponding :code:`End` method retrieves the response from the service and also provides an
opportunity to handle exceptions that might have occurred during the operation.

.. note:: Calling the :code:`End` method is not required. Assuming no errors are encountered, the 
   asynchronous operation will complete whether or not you call :code:`End`.

.. _sdk-net-async-begin-request:

Begin Method Syntax
~~~~~~~~~~~~~~~~~~~

In addition to taking a request object parameter, such as 
:sdk-net-api:`PutItemRequest <DynamoDBv2/TPutItemRequest>`, the async :code:`Begin` methods 
take two additional parameters: a callback function and a state object. Instead of returning a 
:sdk-net-api:`service response object <Runtime/TWebServiceResponse>`, the :code:`Begin` methods 
return a result of type :code:`IAsyncResult`. For the definition of this type, go to the 
`MSDN documentation <http://msdn.microsoft.com/en-us/library/bkbsbb9x.aspx>`_.

*Synchronous Method*

.. code-block:: csharp

    PutItemResponse PutItem(
      PutItemRequest putItemRequest
    )

*Asynchronous Method*

.. code-block:: csharp

    IAsyncResult BeginPutItem( 
      GetSessionTokenRequest getSessionTokenRequest, {AsyncCallback callback}, {Object state}
    )

*AsyncCallback Callback*

The callback function is called when the asynchronous operation is complete. When the function is
called, it receives a single parameter of type 
`IAsyncResult <http://msdn.microsoft.com/en-us/library/bkbsbb9x.aspx>`_. The callback function has 
the following signature.

.. code-block:: csharp

    void Callback(IAsyncResult asyncResult)

*Object State*

The third parameter, :code:`state`, is a user-defined object that is made available to the callback
function as the :code:`AsyncState` property of the :code:`asyncResult` parameter, that is,
:code:`asyncResult.AsyncState`.

*Calling Patterns*

* Passing a callback function and a state object.

* Passing a callback function, but passing null for the state object.

* Passing null for both the callback function and the state object.

This topic provides an example of each of these patterns.

.. _sdk-net-async-waithandle:

Using IAsyncResult.AsyncWaitHandle
""""""""""""""""""""""""""""""""""

In some circumstances, the code that calls the :code:`Begin` method might need to enable another
method that it calls to wait on the completion of the asynchronous operation. In these situations,
it can pass the method the :code:`WaitHandle` returned by the :code:`IAsyncResult.AsyncWaitHandle`
property of the :code:`IAsyncResult` return value. The method can then wait for the asynchronous
operation to complete by calling :code:`WaitOne` on this :code:`WaitHandle`.

.. _sdk-net-async-examples:

Examples
--------

All of the following examples assume the following initialization code.

.. literalinclude:: s3.dotnet.putobject.async.testputobjectasync.start.txt
   :language: csharp
   :dedent: 8

No Callback Specified
~~~~~~~~~~~~~~~~~~~~~

The following example code calls :code:`BeginPutObject`, performs some work, and then calls
:code:`EndPutObject` to retrieve the service response. The call to :code:`EndPutObject` is enclosed
in a :code:`try` block to catch any exceptions that might have been thrown during the operation.

.. literalinclude:: s3.dotnet.putobject.async.testputobjectasync.beginputobject.txt
   :language: csharp
   :dedent: 12

Simple Callback
~~~~~~~~~~~~~~~

This example assumes the following callback function has been defined.

.. literalinclude:: s3.dotnet.putobject.async.simplecallback.txt
   :language: csharp
   :dedent: 8

The following line of code calls :code:`BeginPutObject` and specifies the above callback function.
When the :code:`PutObject` operation is complete, the callback function is called. The call to
:code:`BeginPutObject` specifies :code:`null` for the :code:`state` parameter because the simple
callback function does not access the :code:`AsyncState` property of the :code:`asyncResult`
parameter. Neither the calling code or the callback function call :code:`EndPutObject`. Therefore,
the service response is effectively discarded and any exceptions that occur during the operation are
ignored.

.. literalinclude:: s3.dotnet.putobject.async.testputobjectasync.simplecallback.txt
   :language: csharp
   :dedent: 12

Callback with Client
~~~~~~~~~~~~~~~~~~~~

This example assumes the following callback function has been defined.

.. literalinclude:: s3.dotnet.putobject.async.callbackwithclient.txt
   :language: csharp
   :dedent: 8

The following line of code calls :code:`BeginPutObject` and specifies the preceding callback
function. When the :code:`PutObject` operation is complete, the callback function is called. In this
example, the call to :code:`BeginPutObject` specifies the |S3| client object for the :code:`state`
parameter. The callback function uses the client to call the :code:`EndPutObject` method to retrieve
the server response. Because any exceptions that occurred during the operation will be received when
the callback calls :code:`EndPutObject`, this call is placed within a :code:`try` block.

.. literalinclude:: s3.dotnet.putobject.async.testputobjectasync.callbackwithclient.txt
   :language: csharp
   :dedent: 12

Callback with State Object
~~~~~~~~~~~~~~~~~~~~~~~~~~

This example assumes the following class and callback function have been defined.

.. literalinclude:: s3.dotnet.putobject.async.clientstate.txt
   :language: csharp
   :dedent: 4

.. literalinclude:: s3.dotnet.putobject.async.callbackwithstate.txt
   :language: csharp
   :dedent: 8

The following line of code calls :code:`BeginPutObject` and specifies the above callback function.
When the :code:`PutObject` operation is complete, the callback function is called. In this example,
the call to :code:`BeginPutObject` specifies, for the :code:`state` parameter, an instance of the
:code:`ClientState` class defined previously. This class embeds the |S3| client as well as the time
at which :code:`BeginPutObject` is called. The callback function uses the |S3| client object to call
the :code:`EndPutObject` method to retrieve the server response. The callback also extracts the
start time for the operation and uses it to print the time it took for the asynchronous operation to
complete.

As in the previous examples, because exceptions that occur during the operation are received when
:code:`EndPutObject` is called, this call is placed within a :code:`try` block.

.. literalinclude:: s3.dotnet.putobject.async.testputobjectasync.callbackwithstate.txt
   :language: csharp
   :dedent: 12

.. _sdk-net-async-complete-code:

Complete Sample
---------------

The following code sample demonstrates the patterns you can use when calling the asynchronous
request methods.

.. literalinclude:: s3.dotnet.putobject.async.complete.txt
   :language: csharp

.. _sdk-net-async-see-also:

See Also
--------

* :ref:`net-dg-setup`

* :ref:`net-dg-programming-techniques`




