# OOP
```C#
using System;

namespace Shapes
{
    public abstract class FlatShapes
    {
        public class Position
        {
            public double x;
            public double y;
            public Position(double x0, double y0)
            {
                x = x0;
                y = y0;
            }
            public static bool checkParalell(Position a1, Position a2)
            {
                return Math.Abs(a1.x * a2.y) == Math.Abs(a2.y * a1.x);
            }
            public static double leng(Position a)
            {
                return Math.Sqrt(Math.Pow(a.x, 2) + Math.Pow(a.y, 2));
            }
            public static double Angle(Position a1, Position a2)
            {
                return (a1.x * a2.x + a1.y * a2.y) / (leng(a1) * leng(a2));
            }
            public override string ToString() => $"({x},{y})";
            public static Position operator +(Position a1, Position a2)
            {
                return new Position(a1.x + a2.y, a1.y + a2.y);
            }
            public static Position operator -(Position a1, Position a2)
            {
                return new Position(a1.x - a2.y, a1.y - a2.y);
            }
        }
    }

    interface Iflshape_infor
    {
        public void getPosition();
        public void getArea();
        public void getPerimeter();

    }

    interface Iflshape_calculate
    {
        public double Area();
        public double Perimeter();
    }

    public class triagle : FlatShapes, Iflshape_calculate
    {
        protected double edge1 = 0;
        protected double edge2 = 0;
        protected double edge3 = 0;


        public triagle(Position[] a)
        {
            try
            {
                if (a.Length != 3)
                {
                    Console.WriteLine("Need 3 points to creat a triagle");
                }
                else
                if ((Position.leng(a[0] - a[1]) < Position.leng(a[1] - a[2]) + Position.leng(a[2] - a[0]))
                    || (Position.leng(a[1] - a[2]) < Position.leng(a[0] - a[1]) + Position.leng(a[2] - a[0]))
                    || (Position.leng(a[0] - a[2]) < Position.leng(a[0] - a[1]) + Position.leng(a[1] - a[2]))
                    )
                {
                    edge1 = Position.leng(a[0] - a[1]);
                    edge2 = Position.leng(a[1] - a[2]);
                    edge3 = Position.leng(a[0] - a[2]);
                }
                else throw new Exception();
            }
            catch (Exception)
            {
                Console.WriteLine("Not a triagle");
            }
        }
        public double Perimeter()
        {
            return (edge1 + edge2 + edge3) / 3;
        }
        public double Area()
        {
            return Math.Sqrt(((edge1 + edge2 + edge3) / 2) * (((edge1 + edge2 + edge3) / 2) - edge1) * (((edge1 + edge2 + edge3) / 2) - edge2) * (((edge1 + edge2 + edge3) / 2) - edge3));
        }
        public void getPerimeter()
        {
            Console.WriteLine("Perimeter: " + Perimeter());

        }
        public void getArea()
        {
            Console.WriteLine("Area: " + Area());
        }
        public void info()
        {
            Console.WriteLine("Triagle");
        }

        public class Isosceles : triagle
        {
            public Isosceles(Position[] a) : base(a)
            {
                try
                {
                    if ((Position.leng(a[0] - a[1]) == Position.leng(a[0] - a[2]))
                       || ((Position.leng(a[0] - a[1]) == Position.leng(a[0] - a[2])))
                       || ((Position.leng(a[0] - a[1]) == Position.leng(a[0] - a[2])))
                       )
                    {
                        edge1 = Position.leng(a[0] - a[1]);
                        edge2 = Position.leng(a[1] - a[2]);
                        edge3 = Position.leng(a[0] - a[2]);
                    }
                    else throw new Exception();
                }
                catch (Exception)
                {
                    Console.WriteLine("Not Isosceles");
                }
            }
            public double Perimeter()
            {
                return (edge1 + edge2 + edge3) / 3;
            }
            public double Area()
            {

                return Math.Sqrt(((edge1 + edge2 + edge3) / 2) * (((edge1 + edge2 + edge3) / 2) - edge1) * (((edge1 + edge2 + edge3) / 2) - edge2) * (((edge1 + edge2 + edge3) / 2) - edge3));
            }
            public void getPerimeter()
            {
                Console.WriteLine("Perimeter: " + Perimeter());

            }
            public void getArea()
            {
                Console.WriteLine("Area: " + Area());
            }
            public void info()
            {
                Console.WriteLine("Isosceles");
            }


        }

        sealed class Equilateral : triagle
        {
            public Equilateral(Position[] a) : base(a)
            {
                try
                {
                    if (Position.Angle(a[0] - a[1], a[1] - a[2]) == 1 / 2)
                    {
                        edge1 = Position.leng(a[0] - a[1]);
                    }
                    else throw new Exception();
                }
                catch (Exception)
                {
                    Console.WriteLine("Not Equilateral");
                }
            }
            public double Area()
            {
                return Math.Pow(edge1, 2) * Math.Sqrt(3) / 4;
            }
            public double Perimeter()
            {
                return edge1 * 3;
            }
            public void getPerimeter()
            {
                Console.WriteLine("Perimeter: " + Perimeter());

            }
            public void getArea()
            {
                Console.WriteLine("Area: " + Area());
            }
            public void info()
            {
                Console.WriteLine("Equilateral");
            }

        }


        public class Rectangle : FlatShapes, Iflshape_calculate
        {
            protected double height = 0;
            protected double width = 0;

            public Rectangle(Position[] a)
            {
                try
                {
                    if (a.Length != 4)
                    {
                        Console.WriteLine("Need 4 points to create Rectangle");
                    }
                    else
                    if (Position.checkParalell(a[0] - a[1], a[2] - a[3])
                        && (Position.leng(a[0] - a[1]) == Position.leng(a[2] - a[3]))
                        && (Position.Angle(a[0] - a[1], a[1] - a[2]) == 0)
                        )
                    {
                        height = Position.leng(a[0] - a[1]);
                        width = Position.leng(a[0] - a[1]);
                    }
                    else throw new Exception();
                }
                catch (Exception)
                {
                    Console.WriteLine("Not Rectangle");
                }
            }
            public double Perimeter()
            {
                return (height + width) * 2;
            }
            public double Area()
            {
                return height * width;

            }
            public void getPerimeter()
            {
                Console.WriteLine("Perimeter: " + Perimeter());

            }
            public void getArea()
            {
                Console.WriteLine("Area: " + Area());
            }
            public void info()
            {
                Console.WriteLine("Rectagle");
            }
        }
        sealed class Square : Rectangle
        {
            public Square(Position[] a) : base(a)
            {
                try
                {
                    if (Position.leng(a[0] - a[1]) == Position.leng(a[1] - a[2]))
                    {
                        height = Position.leng(a[0] - a[1]);
                    }
                    else throw new Exception();
                }
                catch (Exception)
                {
                    Console.WriteLine("Not a square!");
                }
            }
            public double erimeter()
            {
                return height * 4;
            }
            public double Area()
            {
                return Math.Pow(height, 2);
            }
            public void getPerimeter()
            {
                Console.WriteLine("Perimeter: " + Perimeter());
            }
            public void getArea()
            {
                Console.WriteLine("Area: " + Area());
            }
            public void info()
            {
                Console.WriteLine("Square");
            }
        }


        class Program
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Shapes");
               
            }

        }
    }
}
    



```
