# JRPrintPreview

[![Build Status](https://travis-ci.com/prsolucoes/jrprintpreview.svg?branch=master)](https://travis-ci.com/prsolucoes/jrprintpreview)  

JasperReports print preview stage class written in JavaFX 12.  

This project is based on this project from **Vitomir Spasojević** but fitted for our needs:
https://github.com/vitomirs/JRPrintPreview

## Usage example

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

## Commands

Some maven commands are available and you can execute it without IDE, including run the sample application:  

```
mvn clean
mvn compile
mvn javafx:run
```

To **package** use:

```
mvn package
```

To check only **dependencies** use:

```
mvn dependency:resolve
```

To **sign** jar file use:

```
mvn jarsigner:sign
```

To **generate jar** file use:

```
mvn clean package
java -jar target/JRPrintPreview-1.0-SNAPSHOT.jar
```

## Generate a key to sign

```
keytool -genkey -keyalg RSA -alias demo -keystore keystore.jks -storepass 123456 -validity 365 -keysize 2048
```

## Requirements

You need Java 12 to run it.  

Obs: If you use Java 8, Java 9 or other you need change file **pom.xml** to 1.8, 1.9 or other version in elements **source**, **target** and **release** of configuration tag.  

## Screenshots

![](extras/screenshots/ss01.png)  
