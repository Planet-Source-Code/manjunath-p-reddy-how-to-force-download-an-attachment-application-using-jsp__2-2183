<div align="center">

## How to force \-download an attachment/application using JSP\.


</div>

### Description

This article along with the code snippet illustrates how to force download an attachment from the server to clients using JSP.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Manjunath P Reddy](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/manjunath-p-reddy.md)
**Level**          |Advanced
**User Rating**    |4.8 (53 globes from 11 users)
**Compatibility**  |Java \(JDK 1\.1\), Java \(JDK 1\.2\)
**Category**       |[Internet/ Browsers/ HTML](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/internet-browsers-html__2-68.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/manjunath-p-reddy-how-to-force-download-an-attachment-application-using-jsp__2-2183/archive/master.zip)





### Source Code

<br>
<b>How to force download of an attachment/application using JSP.</b>
<p>
Many of you guys out there would have experienced the problems associated with the browser interpreting whether to
download an application/attachment or open up in the same browser instance. Whenever microsoft's IE encounters a href tag
pointing to an excel/doc/ppt or any other tool whose plugins have been installed on the client, it opens the attachment
in the same instance of the browser. Hence if a user has to save the file then he has to be smart enuff to click on file
--> save as from the menu and then save to his hard disk.
<p>
But most web-applications are designed for ease and not keeping the user's technical skill or knowledge in view. Hence
when a user clicks on a href(which might say click to download pdf version) pointing to say mydownloadable.pdf, what
happens is the pdf downloads the file to his temporary internet files and shows it in the browser.
<p>
The code snippet below shows how one can force download a file/app/attachment to the user irrespective of whether the
user has a necessary plugin or not. Even the name of the downloaded file can be specified dynamically.
<br><br>
<pre>
&lt;!--contents of download.jsp--&gt;
&lt;%@ page import="java.util.*,java.io.*"%&gt;
&lt;!--Assumes that file name is in the request objects query Parameter --&gt;
&lt;%
	//read the file name.
	File f = new File ("c:/fop/mypdf/" + request.getParameter("file") );
	//set the content type(can be excel/word/powerpoint etc..)
	response.setContentType ("application/pdf");
	//set the header and also the Name by which user will be prompted to save
	response.setHeader ("Content-Disposition", "attachment;
filename=\"LicenseAgreement.pdf\"");
	//get the file name
	String name = f.getName().substring(f.getName().lastIndexOf("/") + 1,f.getName().length());
	//OPen an input stream to the file and post the file contents thru the
	//servlet output stream to the client m/c
		InputStream in = new FileInputStream(f);
		ServletOutputStream outs = response.getOutputStream();
		int bit = 256;
		int i = 0;
		try {
			while ((bit) >= 0) {
				bit = in.read();
				outs.write(bit);
			}
			//System.out.println("" +bit);
		} catch (IOException ioe) {
			ioe.printStackTrace(System.out);
		}
//		System.out.println( "\n" + i + " bytes sent.");
//		System.out.println( "\n" + f.length() + " bytes sent.");
		outs.flush();
		outs.close();
		in.close();
%>
</pre>
<br>
Hope you find this useful...
<br>
Adios and Happy Programming!!!<br>
-------------------------------------------------------<br>
Carved upon my stone, My body lies but still I roam...<br>
Manjunath P Reddy

