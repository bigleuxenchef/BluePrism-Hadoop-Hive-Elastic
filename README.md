# BluePrism-Hadoop-Hive-Elastic
This project aims at testing and providing insight on how to integrate BluePrism with Hadoop and Elasticsearch Stack
As I am a fa experimenting, I like to install everything by myself, this is a way to get to understand thing under the hood. Here are the list of software installed in my sand box for this project :

**Installed on Linux**
 - Hadoop 2.7.3
  - Spark 2.2.1
 - Hive 2.1.0
 - Oozie 4.3.0 (optional)
 - Hue 3.12.0
 - Elastic 6.x, Kibana 6.x

**Installed on Windows**

  - Microsoft® Hive ODBC Driver

# Testing Hadoop/Hive

First make sure you have everything you need in *hadoop*, I use *hue* tool s very friendly rather than the *hadoop* command shell. Furthermore as we are going to use hive as the proxy to get access to all data, it is important to visualize that everything works fine.

## Hue

<img src="./images/hue-3.12.0.png" width=100% align="middle">

## Sample of using Hive to access Elastic table from Hue

<img src="./images/hue-elastictable.png" width=100% align="middle">

## Sample using shell beeline to get to hive.

<img src="./images/beeline-hive.png" width=100% align="middle">

# Configure ODBC

Be careful to chose what works with your application *ODBC 32 bit* or *64 bit*, here is the configuration that works for me.

<img src="./images/ODBCConf.png" width=30% align="middle">


# Testing C# first

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;
using System.Data.Common;

namespace HiveTest
{
    class Program
    {
        static void Main(string[] args)
        {
            GetData();
            Console.WriteLine("----------------------------------------------");
            Console.WriteLine("Press a key to end");
            Console.Read();
        }
        static async void GetData()
        {
            using (OdbcConnection conn =
                   new OdbcConnection("DSN=MyHiveLocal"))
            {
                object[] meta = new object[10];
                bool read;
                conn.Open();
                OdbcCommand cmd = conn.CreateCommand();

                OdbcCommand cmd2 = conn.CreateCommand();

                
                cmd.CommandText =
                    "select * from rumi.blueprism limit 10;";
                    //"select * from rumi.customers limit 10;";
                //"show databases;use rumi;show tables;select * from rumi.droolsset;";
                DbDataReader dr =  cmd.ExecuteReader();
                System.Data.DataTable tmpHiveTable = dr.GetSchemaTable();
                if (dr.Read() == true)
                {
                    do
                    {
                        int NumberOfColums = dr.GetValues(meta);

                        for (int i = 0; i < NumberOfColums; i++)
                            Console.Write("{0} ", meta[i].ToString());

                        Console.WriteLine();
                        read = dr.Read();
                    } while (read == true);
                }
                dr.Close();

            }
        }
    }
}


```

### Output

<img src="./images/charpoutput.png" width=100% align="middle">






