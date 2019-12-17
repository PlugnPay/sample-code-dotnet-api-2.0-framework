====================================================
PlugnPay .Net Version 2.0 DLL
created on 09/30/2009
====================================================

***** IMPORTANT NOTES *****
This DLL is being provided "AS IS".  Limited technical support assistance will
be given to help diagnose/address problems with this DLL.  The amount of support
provided is up to PlugnPay's staff.

It is recommended if you experience a problem with this DLL, first seek assistance
through this DLL's readme file, then check with the MSDN developer forum, and if you
are still unable to resolve the issue, contact us via PlugnPay's Online Helpdesk.

You will required to supply your login username/password for payment processing.
The authorization will be done via PlugnPay's API payment method.  The DLL is
intended to take advantage of .Net Version 2.0's ability to connect to PlugnPay's 
payment gateway for payment processing,

If you want to change the behavior of this DLL, please feel free to make changes
to the files yourself.  However, customized DLL modules will not be provided
support assistance.

***************************



1.  Implementing the DLL

The PnPSend.dll just needs to be added as a reference to your .Net application.  Once that is done you just need to declare a new variable as type "PnPSend.Plugnpay".



2.  Using the DLL

There are two different functions written into the DLL the first one is a simple function which will return the DLL version number.  This is simply called "version".  The second function is "PnPSend" which has two inputs Params and URL.  Params is a string which contains your transaction's information using the standard found on our Remote Client Integration Specification which can be found by going to your administration area and clicking on the Documentation/FAQ link.  The other input is the submission URL, which by default is set to the proper URL, but if you needed to override it for any reason you can, just by entering the new URL in this input.

When you call the DLL it will take your string and submit it to our secure server.  The entire process uses SSL encryption so it is done safely.  The DLL will then return a string containing the server's response and/or an error message if there was a problem.  This DLL will automatically encode your string before sending it and decode it before returning it back to you.  The only time additional decoding is required would be if you are running a transaction which contains multiple levels of data (such as a Query_trans).  If a transaction does contain multiple levels we will have its upper levels decoded automatically but each of the lower levels will need to be manually decoded outside of the DLL (sample source code can be found in section 4b).


3.  Troubleshooting

Type 'PnPSend.Plugnpay' is not defined
This error is caused when a reference to the PnPSend.dll file has not been made.

pnpcom_err=Non HTTPS URL
This means that the custom URL you have entered is not an HTTPS URL and can have the information sent to it.

pnpcom_err=No Params
No string was passed to the API for processing



4.  Sample Code 

4a. Auth Sample Code
The code below will allow you to use the PnPSend DLL to send a simple auth to our system.  To use this sample you just need to create a new form with two textboxes and a button.  Once you create that you need to add the reference to PnPSend.dll and paste the sample code below into the form coding section.

    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
	Dim a As New PnPSend.Plugnpay
        TextBox2.Clear() 'Clears textbox2
        Dim TempArray = Split(a.PnPSend(TextBox1.Text), "&") 'Breaks up the results from PnPSend into an array using '&' to determine each field
        Dim i As Integer
        While i < TempArray.length
            TextBox2.Text += TempArray(i) & vbNewLine 'write out each field and a newline
            i += 1
        End While
    End Sub


4b. Query_trans Sample Code
The code below will allow you to use the PnPSend DLL to send a query trans and to loop through the results and decode them.  To use this sample you just need to create a new form with one textbox, a listbox and a button.  Once you create that you need to add the reference to PnPSend.dll and paste the sample code below into the form coding section.

    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
	Dim a As New PnPSend.Plugnpay
        ListBox1.Items.Clear() 'clears out the listbox
        Dim TempArray = Split(a.PnPSend(TextBox1.Text), "&") 'Breaks up the results from PnPSend into an array using '&' to determine each field
        Dim i As Integer
        While i < TempArray.length
            ListBox1.Items.Add(System.Web.HttpUtility.UrlDecode(TempArray(i))) 'write out each field and a newline and decode
            i += 1
        End While
    End Sub

====================================================
PlugnPay .Net Version 2.0 DLL
Version History

- created on 09/30/2009
- modified on 10/08/2009 to be better compatible with C#

====================================================