# Platforms Supported by the AWS SDK for \.NET<a name="net-dg-platform-diffs-v3"></a>

The AWS SDK for \.NET provides distinct groups of assemblies for developers to target different platforms\. However, not all SDK functionality is the same on each of these platforms\. This topic describes the differences in support for each platform\.<a name="net-dg-platform-diff-netfx35"></a>

## \.NET Framework 4\.5<a name="net-dg-platform-diff-netfx45"></a>

This version of the AWS SDK for \.NET is compiled against \.NET Framework 4\.5 and runs in the \.NET 4\.0 runtime\. AWS service clients support synchronous and asynchronous calling patterns and use the [async and await](http://msdn.microsoft.com/en-us/library/vstudio/hh191443.aspx) keywords introduced in [C\# 5\.0](https://en.wikipedia.org/wiki/C_Sharp_%28programming_language%29#Versions)\.

## \.NET Framework 3\.5<a name="net-dg-platform-diff-winrt"></a>

This version of the AWS SDK for \.NET is compiled against \.NET Framework 3\.5, and runs either the \.NET 2\.0 or \.NET 4\.0 runtime\. AWS service clients support synchronous and asynchronous calling patterns and use the older Begin and End pattern\.

**Note**  
The AWS SDK for \.NET is not Federal Information Processing Standard \(FIPS\) compliant when used by applications built against version 2\.0 of the CLR\. For details on how you can substitute a FIPS compliant implementation in that environment, refer to [CryptoConfig](https://blogs.msdn.microsoft.com/shawnfa/2008/12/02/cryptoconfig/) on the Microsoft blog and the [CLR Security](http://clrsecurity.codeplex.com/) team’s HMACSHA256 class \( HMACSHA256Cng \) in Security\.Cryptography\.dll\.

## \.NET Core<a name="net-core"></a>

The AWS SDK for \.NET supports applications written for \.NET Core\. AWS service clients only support asynchronous calling patterns in \.NET core\. This also affects many of the high level abstractions built on top of service clients like Amazon S3’s `TransferUtility` which will only support asynchronous calls in the \.NET Core environment\. For details, see [Configuring the AWS SDK for \.NET with \.NET Core](net-dg-config-netcore.md)\.

## Portable Class Library<a name="portable-class-library"></a>

The AWS SDK for \.NET also contains a Portable Class Library implementation\. The Portable Class Library implementation can target multiple platforms,including Universal Windows Platform \(UWP\), and Xamarin on iOS and Android\. See the AWS Mobile SDK for \.NET and Xamarin for more details\. AWS service clients only support asynchronous calling patterns\.

## Unity Support<a name="unity-support"></a>

The AWS SDK for \.NET supports generating Assemblies for Unity\. More information can be found in the [Unity README](https://github.com/aws/aws-sdk-net/blob/master/Unity.README.md)\.

## More Info<a name="more-info"></a>
+  [Migrating Your Code to Version 3 of the AWS SDK for \.NET](migration-v3.md) 