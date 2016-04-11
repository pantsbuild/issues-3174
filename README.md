This repo serves as a minimal example of the problems described in
https://github.com/pantsbuild/pants/issues/3174.

To test, 1st run `./pants` to get pants bootstrapped and then  apply
`pants.patch` to your cached pants `0.0.81` version under `~/.cache/pants/...`.

With this patch in place, you should find something like:
```
$ ./pants clean-all resolve ::
fatal: ambiguous argument 'HEAD': unknown revision or path not in the working tree.
Use '--' to separate paths from revisions, like this:
'git <command> [<revision>...] -- [<file>...]'
INFO] Failed to load git repository at /home/jsirois/dev/pantsbuild/issues-3174: git --git-dir=/home/jsirois/dev/pantsbuild/issues-3174/.git --work-tree=/home/jsirois/dev/pantsbuild/issues-3174 rev-parse --abbrev-ref HEAD failed with exit code 128

19:58:22 00:00 [main]
               See a report at: http://localhost:35244/run/pants_run_2016_04_10_19_58_22_328_7d3fb360f9a1469d8916d170b4b4eef4
19:58:22 00:00   [setup]
19:58:22 00:00     [parse]fatal: ambiguous argument 'HEAD': unknown revision or path not in the working tree.
Use '--' to separate paths from revisions, like this:
'git <command> [<revision>...] -- [<file>...]'
INFO] Failed to load git repository at /home/jsirois/dev/pantsbuild/issues-3174: git --git-dir=/home/jsirois/dev/pantsbuild/issues-3174/.git --work-tree=/home/jsirois/dev/pantsbuild/issues-3174 rev-parse --abbrev-ref HEAD failed with exit code 128

               Executing tasks in goals: clean-all -> bootstrap -> imports -> unpack-jars -> deferred-sources -> jvm-platform-validate -> gen -> resolve
19:58:22 00:00   [clean-all]
19:58:22 00:00     [ng-killall]
19:58:22 00:00     [clean-all]
19:58:22 00:00     [kill-pantsd]
19:58:22 00:00   [bootstrap]
19:58:22 00:00     [jar-dependency-management]
19:58:22 00:00     [bootstrap-jvm-tools]
19:58:22 00:00   [imports]
19:58:22 00:00     [ivy-imports]
19:58:22 00:00   [unpack-jars]
19:58:22 00:00     [unpack-jars]
19:58:22 00:00   [deferred-sources]
19:58:22 00:00     [deferred-sources]
19:58:22 00:00   [jvm-platform-validate]
19:58:22 00:00     [jvm-platform-validate]
19:58:22 00:00   [gen]
19:58:22 00:00     [thrift]
19:58:22 00:00     [protoc]
19:58:22 00:00     [antlr]
19:58:22 00:00     [ragel]
19:58:22 00:00     [jaxb]
19:58:22 00:00     [wire]
19:58:22 00:00   [resolve]
19:58:22 00:00     [ivy]
19:58:22 00:00       [cache] 
19:58:22 00:00       [bootstrap-nailgun-server]
                     ==== stderr ====
                     Exception in thread "main" java.text.ParseException: failed to load settings from file:/home/jsirois/dev/pantsbuild/issues-3174/ivysettings.xml: no default constructor on class ohnosequences.ivy.S3Resolver for adding s3resolver on class org.apache.ivy.plugins.resolver.ChainResolver
                      at org.apache.ivy.core.settings.XmlSettingsParser.doParse(XmlSettingsParser.java:165)
                      at org.apache.ivy.core.settings.XmlSettingsParser.parse(XmlSettingsParser.java:150)
                      at org.apache.ivy.core.settings.IvySettings.load(IvySettings.java:393)
                      at org.apache.ivy.Ivy.configure(Ivy.java:417)
                      at org.apache.ivy.Main.initSettings(Main.java:452)
                      at org.apache.ivy.Main.run(Main.java:247)
                      at org.apache.ivy.Main.main(Main.java:219)
                     Caused by: java.lang.IllegalArgumentException: no default constructor on class ohnosequences.ivy.S3Resolver for adding s3resolver on class org.apache.ivy.plugins.resolver.ChainResolver
                      at org.apache.ivy.util.Configurator.startCreateChild(Configurator.java:531)
                      at org.apache.ivy.core.settings.XmlSettingsParser.inConfiguratorStarted(XmlSettingsParser.java:579)
                      at org.apache.ivy.core.settings.XmlSettingsParser.startElement(XmlSettingsParser.java:201)
                      at com.sun.org.apache.xerces.internal.parsers.AbstractSAXParser.startElement(AbstractSAXParser.java:509)
                      at com.sun.org.apache.xerces.internal.parsers.AbstractXMLDocumentParser.emptyElement(AbstractXMLDocumentParser.java:182)
                      at com.sun.org.apache.xerces.internal.impl.XMLDocumentFragmentScannerImpl.scanStartElement(XMLDocumentFragmentScannerImpl.java:1344)
                      at com.sun.org.apache.xerces.internal.impl.XMLDocumentFragmentScannerImpl$FragmentContentDriver.next(XMLDocumentFragmentScannerImpl.java:2787)
                      at com.sun.org.apache.xerces.internal.impl.XMLDocumentScannerImpl.next(XMLDocumentScannerImpl.java:606)
                      at com.sun.org.apache.xerces.internal.impl.XMLDocumentFragmentScannerImpl.scanDocument(XMLDocumentFragmentScannerImpl.java:510)
                      at com.sun.org.apache.xerces.internal.parsers.XML11Configuration.parse(XML11Configuration.java:848)
                      at com.sun.org.apache.xerces.internal.parsers.XML11Configuration.parse(XML11Configuration.java:777)
                      at com.sun.org.apache.xerces.internal.parsers.XMLParser.parse(XMLParser.java:141)
                      at com.sun.org.apache.xerces.internal.parsers.AbstractSAXParser.parse(AbstractSAXParser.java:1213)
                      at com.sun.org.apache.xerces.internal.jaxp.SAXParserImpl$JAXPSAXParser.parse(SAXParserImpl.java:643)
                      at com.sun.org.apache.xerces.internal.jaxp.SAXParserImpl.parse(SAXParserImpl.java:327)
                      at javax.xml.parsers.SAXParser.parse(SAXParser.java:274)
                      at org.apache.ivy.core.settings.XmlSettingsParser.doParse(XmlSettingsParser.java:160)
                      ... 6 more
                     
                     ==== stdout ====
                     :: loading settings :: file = /home/jsirois/dev/pantsbuild/issues-3174/ivysettings.xml
                     
19:58:22 00:00   [complete]
               FAILURE
Exception caught: (<class 'pants.backend.jvm.ivy_utils.IvyError'>)

Exception message: Ivy returned 1. cmd=/usr/bin/java -Dsun.io.useCanonCaches=false -Divy.cache.dir=/home/jsirois/.ivy2/pants -cp ../../../.ivy2/pants/org.apache.ivy/ivy/jars/ivy-2.4.0.jar:../../../.ivy2/pants/co.actioniq.thirdparty.ohnosequences/ivy-s3-resolver/jars/ivy-s3-resolver-0.8.0.jar:../../../.ivy2/pants/com.amazonaws/aws-java-sdk-s3/jars/aws-java-sdk-s3-1.10.47.jar:../../../.ivy2/pants/com.amazonaws/aws-java-sdk-kms/jars/aws-java-sdk-kms-1.10.47.jar:../../../.ivy2/pants/com.amazonaws/aws-java-sdk-core/jars/aws-java-sdk-core-1.10.47.jar:../../../.ivy2/pants/commons-logging/commons-logging/jars/commons-logging-1.1.3.jar:../../../.ivy2/pants/org.apache.httpcomponents/httpclient/jars/httpclient-4.3.6.jar:../../../.ivy2/pants/org.apache.httpcomponents/httpcore/jars/httpcore-4.3.3.jar:../../../.ivy2/pants/commons-codec/commons-codec/jars/commons-codec-1.6.jar:../../../.ivy2/pants/com.fasterxml.jackson.core/jackson-databind/bundles/jackson-databind-2.5.3.jar:../../../.ivy2/pants/com.fasterxml.jackson.core/jackson-annotations/bundles/jackson-annotations-2.5.0.jar:../../../.ivy2/pants/com.fasterxml.jackson.core/jackson-core/bundles/jackson-core-2.5.3.jar:../../../.ivy2/pants/joda-time/joda-time/jars/joda-time-2.8.1.jar org.apache.ivy.Main -settings /home/jsirois/dev/pantsbuild/issues-3174/ivysettings.xml -ivy /home/jsirois/dev/pantsbuild/issues-3174/.pants.d/ivy/927dd8e6d93a108a642a4aa4bf20f1f39430b311-IvyResolveFingerprintStrategy_53c4bb9c6553/resolve-ivy.xml -confs default -cachepath /home/jsirois/dev/pantsbuild/issues-3174/.pants.d/ivy/927dd8e6d93a108a642a4aa4bf20f1f39430b311-IvyResolveFingerprintStrategy_53c4bb9c6553/classpath.raw.tmp.722963e728d44926be22f89a0bca7601
```

So there are 2 issues here:

1. Modifying pants ivy bootstrapping to allow use of a different (or `None` / the default)
   `ivysettings.xml` for ivy classpath bootstrapping.
2. The `ohnosequences.ivy.S3Resolver` resolver needs a wrapper class with a default constructor
   (and possibly other modifications) that can be instantiated by ivy and configured via
   `ivysettings.xml`.

