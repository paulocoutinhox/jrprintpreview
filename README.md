# JRPrintPreview

[![Build Status](https://travis-ci.com/prsolucoes/jrprintpreview.svg?branch=master)](https://travis-ci.com/prsolucoes/jrprintpreview)  

JasperReports print preview stage class written in JavaFX 12  

### Usage example

Whole functionality is contained in a `JRPrintPreview.java` file. This file should be copied to your project. The rest of the files represent an example project which demonstrates print preview functionality for one simple JasperReports report.

Basic usage is shown in the next example.

```
String reportFileName = "SomeReport.jasper";
Map<String, Object> paramMap = new HashMap<>();
JRBeanCollectionDataSource dataSource = new JRBeanCollectionDataSource(...);

JasperReport jasperReport = (JasperReport) JRLoader.loadObject(
	JRLoader.getResourceInputStream(reportFileName)
);

JasperPrint jasperPrint = JasperFillManager.fillReport(
	jasperReport, paramMap, dataSource
);

JRPrintPreview printPreview = new JRPrintPreview(jasperPrint);
printPreview.show();
```

### Commands

You can use all from maven without IDE if you want

```
mvn clean
mvn compile
mvn install
mvn javafx:run
```

### Requirements

You need Java 12 to run it.  

If you use Java 8 or Java 9 you need change file **pom.xml** to 1.8 or 1.9 version.  


### Screenshot

![](extras/screenshots/ss01.png)  
