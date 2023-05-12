# hesabdari
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp5
{
    struct infoKala
    {
        public string name;
        public string info;
        public int date;
        public int price;
        public int code;
        public int count;
    }
    struct SoldItem
    {
        
        public infoKala kala;
        public string TheBuyer;
        public int price;
        public int count;
        public int SaleDate;
        public int code;
    }
    struct ChekInfo
    {
        public string ChekOwner;
        public string PayTo;
        public int PriceChek;
        public int SerialNumber;
        public int date;

    }
    class Program
    {
        List<infoKala> ListKala = new List<infoKala>();
        List<SoldItem> SalesList = new List<SoldItem>();
        List<ChekInfo> chekList = new List<ChekInfo>();
        int SunPriceKala = 0;
        int SunCountKala = 0;

        static void Main(string[] args)
        {
            Program b = new Program();

            bool flag = true;
            int readNum = 0;
            string pass = "";
            Console.WriteLine("enter password");
            pass = Console.ReadLine();

            bool xrp = true;

            while (xrp)
            {

                if (pass == "1234")
                {

                    b.c();
                    xrp = false;
                }
                else
                {
                    Console.WriteLine("enter the correct password");
                    pass = Console.ReadLine();


                }




            }

            Console.ReadKey();
        }
        public infoKala info()
        {

            infoKala ins = new infoKala();
            //نام کالا
            Console.WriteLine("enter name");
            ins.name = Console.ReadLine();
            //قیمت کالا
            Console.WriteLine("enter price");

            ins.price = getInt();
            //توضیحات کالا
            Console.WriteLine("enter info ");
            ins.info = Console.ReadLine();
            //سال تولید
            Console.WriteLine("enter date");

            ins.date = getInt();
            //کد کالا
            Console.WriteLine("enter code");

            ins.code = getInt();
            //تعداد کالا
            Console.WriteLine("enter count kala");
            ins.count = getInt();

            return ins;





        }
        public void addKala()
        {

            ListKala.Add(info());



        }

        public void sortKala()
        {
            for (int i = 1; i < ListKala.Count; i++)
            {
                for (int j = 0; j < ListKala.Count - i; j++)
                {
                    infoKala temp = new infoKala();
                    if (ListKala[j].price > ListKala[j + 1].price)
                    {
                        temp = ListKala[j];
                        ListKala[j] = ListKala[j + 1];
                        ListKala[j + 1] = temp;
                    }

                }
            }

        }
        public void ShowListKala()
        {
            foreach (infoKala item in ListKala)
            {
                print(item);
            }
        }
        public infoKala getKala()
        {
            bool loop = true;
            infoKala kala = new infoKala();
            while (loop)
            {
                int code1;
                Console.WriteLine("enter code kala");
                code1 = getInt();

                kala = ListKala.Where(p => p.code == code1).SingleOrDefault();

                if (kala.code == 0)
                {
                    Console.WriteLine("kala not found kala enter 1 for continiue");
                    if (getInt() != 1)
                    {
                        loop = false;
                    }
                }

                else
                    loop = false;

            }



            return kala;
        }


        public int getInt()
        {
            bool flag = false;
            int num = 0;
            while (true)
            {
                string str = Console.ReadLine();
                flag = tryPars(str, out num);
                if (flag == true)
                {
                    return num;
                }

                Console.WriteLine("enter corect number");
            }

        }
        public bool tryPars(string a, out int o)
        {

            foreach (char c in a.ToArray())
            {
                if ((c >= 48 && c <= 57) == false)
                {
                    o = 0;
                    return false;
                }


            }
            o = Convert.ToInt32(a);

            return true;

        }
        public void sortKala2()
        {
            for (int i = 1; i < ListKala.Count; i++)
            {
                for (int j = 0; j < ListKala.Count - i; j++)
                {
                    infoKala temp = new infoKala();
                    if (ListKala[j].price < ListKala[j + 1].price)
                    {
                        temp = ListKala[j];
                        ListKala[j] = ListKala[j + 1];
                        ListKala[j + 1] = temp;

                    }

                }
            }
        }

        public void Expensive()
        {

            if (ListKala.Count == 0)
                return;
            sortKala();

            infoKala fhd = ListKala[ListKala.Count - 1];
            print(fhd);


        }
        public void chepeer()
        {
            if (ListKala.Count == 0)
                return;
            sortKala();

            infoKala fhd = ListKala[0];
            print(fhd);

        }
        public void print(infoKala item)
        {
            Console.WriteLine("name: " + item.name + "  info Kala: " + item.info + "  price kala: " + item.price.ToString() + " countc kala= " + item.count.ToString());

        }
        public void sun()
        {
            SunCountKala = 0;
            SunPriceKala = 0;
            double avg = 0;
            foreach (infoKala hdh in ListKala)
            {
                SunCountKala = SunCountKala + hdh.count;
                SunPriceKala = SunPriceKala + hdh.price * hdh.count;

            }
            avg = SunPriceKala / SunCountKala;


            Console.WriteLine("sun price kala= " + SunPriceKala + " sun count kala= " + SunCountKala + " avg kala= " + avg);

        }
        public SoldItem sale(infoKala objIn)
        {
            SoldItem far = new SoldItem();
            //نام کالای برای فروش
            Console.WriteLine(" name  Kala : " + objIn.name);

            //تعداد کالا برای فروش
            Console.WriteLine("count Kala : " + objIn.count.ToString());


            far.kala = new infoKala();
            far.kala = objIn;
            //نام خریدار
            Console.WriteLine("enrer name buyer");
            far.TheBuyer = Console.ReadLine();
            //قیمت فروخته شده
            Console.WriteLine("enter price");
            far.price = getInt();
            //تعداد کالا
            Console.WriteLine("enter count Kala");
            far.count = getInt();
            //تاریخ فروش کالا
            Console.WriteLine("enter data");
            far.SaleDate = getInt();
            //کد ملی خریدار
            Console.WriteLine("enter code meli buyer");
            far.code = getInt();

            return far;
        }
        public void AddSoldKala()
        {
            SoldItem sold = new SoldItem();
            infoKala kala = new infoKala();
            infoKala kal = getKala();
            if (kal.code > 0)
            {
                sold = sale(kal);
            }
            if (sold.count > 0 && kal.count > sold.count)
            {
                kala.count = kala.count - sold.count;

                

                SalesList.Add(sold);
                Console.WriteLine("it is registered");
            }
            else
                Console.WriteLine("the information is incorrect");
            
        }
        public infoKala findKalaToSale()
        {
            Console.WriteLine("enter code for sale");

            infoKala obj = getKala();

            return obj;


        }

        public void ShowListSales()
        {
            foreach (SoldItem kala in SalesList)
            {
                Console.WriteLine("name kala = " + kala.kala.name + " name buyer= " + kala.TheBuyer +
                    " price kala=" + kala.price.ToString() + " date sale= " + kala.SaleDate.ToString() + "code meli buyer= " + kala.code.ToString());
            }
        }
        public void SellMenu()
        {
            bool erd = true;
            int num = 0;
            while (erd == true)
            {
                Console.WriteLine("enter 1 for add kala");
                Console.WriteLine("enter 2 for exit");

                num = Convert.ToInt32(Console.ReadLine());
                if (num == 1)
                {
                    AddSoldKala();
                }
                else if (num == 2)
                {
                    erd = false;
                }
            }
        }
        public ChekInfo chek()
        {
            ChekInfo frt = new ChekInfo();
            //مالک چک
            Console.WriteLine("Chek owner:  ");
            frt.ChekOwner = Console.ReadLine();
            //در وجه
            Console.WriteLine("pay to: ");
            frt.PayTo = Console.ReadLine();
            //قیمت چک
            Console.WriteLine("price Chek: ");
            frt.PriceChek = getInt();
            //شماره سریال چک
            Console.WriteLine("serial number chek: ");
            frt.SerialNumber = getInt();
            //تاریخ چک
            Console.WriteLine("date: ");
            frt.date = getInt();

            return frt;



        }
        public void AddChek()
        {
            chekList.Add(chek());
        }
        public void ChekMenu()
        {
            bool fsd = true;
            int num = 0;
            while (fsd == true)
            {


                Console.WriteLine("enter 1 for add chek");
                Console.WriteLine("enter 2 for exit");

                num = Convert.ToInt32(Console.ReadLine());

                if (num == 1)
                {
                    AddChek();
                }
                if (num == 2)
                {
                    fsd = false;
                }
            }

        }
        public void c()
        {
            int readNum = 0;
            bool flag = true;
            while (flag == true)
            {


                Console.WriteLine("enter 1 for insert kala");
                Console.WriteLine("enter 2  for sort kala");
                Console.WriteLine("enter 3  for Show list kala");
                Console.WriteLine("enrer 4 for sort kala2");
                Console.WriteLine("enter 5  for expensive kala");
                Console.WriteLine("enter 6 for Chepeer kala");
                Console.WriteLine("enter 7 for price kala & count kala");
                Console.WriteLine("enter 8 for add sold kala");
                Console.WriteLine("enter 9 for Show List sales");
                Console.WriteLine("enter 10 for add chek");
                Console.WriteLine("enter 11 for exit");

                readNum = Convert.ToInt32(Console.ReadLine());

                if (readNum == 1)
                {
                    addKala();
                }
                else if (readNum == 2)
                {
                    sortKala();
                }
                else if (readNum == 3)
                {
                    ShowListKala();
                }
                else if (readNum == 4)
                {
                    sortKala2();
                }
                else if (readNum == 5)
                {
                    Expensive();
                }
                else if (readNum == 6)
                {
                    chepeer();
                }
                else if (readNum == 7)
                {
                    sun();
                }
                else if (readNum == 8)
                {
                    SellMenu();
                }
                else if (readNum == 9)
                {
                    ShowListSales();
                }
                else if (readNum == 10)
                {
                    ChekMenu();
                }
                else if (readNum == 11)
                {
                    Income();
                }
            }

        }
        public void Income()
        {
            SoldItem sold = new SoldItem();
            infoKala kal = new infoKala();
            int Incom = 0;
            
            
                Incom =  sold.price * sold.count;
                Console.WriteLine( "in"+sold.SaleDate+"Income: "+Incom );
            
        }
       

    }

}

           
        


        


    
 

    
