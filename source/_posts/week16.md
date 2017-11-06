---
title: week16
date: 2017-11-05 21:46:51
tags: Work Log
password: tswc941=
---

I came cross a very bizarre case. I can successfuly build in intellij but when I use brazil build, it failed. It camplains that in the file: `AudiblePaymentsWidgetApplication/src/test/java/com/audible/paymentswidget/datasources/PaymentsWidgetDataSourceTest.java` cannot find symbol `import com.audible.payments.utilities.AudiblePaymentUtilsImpl;` However, we can find the file in `AudibleAddressAndPaymentsLib`. The problem is normally we should not use 

```java
private PaymentUtils paymentUtils = new AudiblePaymentUtilsImpl();
``` 

in the test code. We should mock all the services and utils in other packages. Because brazil build should only compile the code and only run the code in current package rather than create an instance from other packages. In the `Config` file, we can find `AudibleAddressAndPaymentsLib` is in runtime-dependencies. We should not create instances in `AudibleAddressAndPaymentsLib` when we build the `AudiblePaymentsWidgetApplication` package. 

However, this kind of error only occured when we turn on the find bug. If we turn findbug off, it would be like we run in intellij, the brazil build will find the dependency automatically, even though it is not perfectly correctly.