# Repositorio Base para Moldex

```c#
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Net;
using System.Windows.Forms;
using System.IO;

namespace Test14Nov
{
	public partial class Form1 : Form
	{
    	public Form1()
    	{
        	InitializeComponent();
    	}

    	private void button1_Click(object sender, EventArgs e)
    	{
       	 
        	var httpWebRequest = (HttpWebRequest)WebRequest.Create("https://6l58zmqdzf.execute-api.us-east-1.amazonaws.com/HelloThere");
        	httpWebRequest.ContentType = "application/json";
        	httpWebRequest.Method = "POST";

        	using (var streamWriter = new StreamWriter(httpWebRequest.GetRequestStream()))
        	{
            	string json = "{\"user\":\"test\"," +
                          	"\"password\":\"bla\"}";

            	streamWriter.Write(json);
        	}

        	var httpResponse = (HttpWebResponse)httpWebRequest.GetResponse();
        	using (var streamReader = new StreamReader(httpResponse.GetResponseStream()))
        	{
            	var result = streamReader.ReadToEnd();
            	label1.Text = result;
        	}
       	 
    	}
	}
}



```
