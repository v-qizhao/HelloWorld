````VB.NET
	Public Class MvcApplication
	  Inherits System.Web.HttpApplication
	  ...
	  Private Shared Sub ConfigureTraceListener()
	    Dim enableTraceListener As Boolean = False
	    Dim enableTraceListenerSetting As String = RoleEnvironment.GetConfigurationSettingValue("EnableTableStorageTraceListener")
	    If Boolean.TryParse(enableTraceListenerSetting, enableTraceListener) Then
	      If enableTraceListener Then
	        Dim listener As New AzureDiagnostics.TableStorageTraceListener("Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString") With {.Name = "TableStorageTraceListener"}
	        System.Diagnostics.Trace.Listeners.Add(listener)
	        System.Diagnostics.Trace.AutoFlush = True
	      Else
	        System.Diagnostics.Trace.Listeners.Remove("TableStorageTraceListener")
	      End If
	    End If
	  End Sub
	End Class
````
