# Faris_Abdullah
&lt;Name>







using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Threading;

namespace ConsoleApp1
{
    class Program
    {
        private static Mutex mutex = new Mutex();
        static void Main(string[] args)
        {
            for (int i = 0; i < 10; i++)
            {
                Thread t = new Thread(new ThreadStart(MutexDemo));
                t.Name = string.Format("Thread {0} :", i + 1);
                t.Start();
            }
            Console.ReadKey();
        }
        static void MutexDemo()
        {
            try
            {
                mutex.WaitOne();   // Wait until it is safe to enter.  
                Console.WriteLine("{0} telah masuk ke dalam Domain", Thread.CurrentThread.Name);
                Thread.Sleep(1000);    // Wait until it is safe to enter.  
                Console.WriteLine("{0} meninggalkan Domain\r\n", Thread.CurrentThread.Name);
            }
            finally
            {
                mutex.ReleaseMutex();
            }
        }   
    }
}

