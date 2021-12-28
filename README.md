# vmat-port
Постановка задачи: составить программу, которая реализует численные методы решения дифференциальных уравнений (метод Эйлера, метод Рунге-Кутта, дифференциальные уравнения второго порядка, система дифференциальных уравнений). Программа должна содержать меню выбора конкретного метода.

```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

float fdy(float xf, float yf)
{
  float d = yf * (1 - xf);
  return d;
}

void m_eiler() //метод Эйлера
{
  float a, b, y, h, x;
  int n; 
  printf("Euler Method\n\n");
  printf("Enter a number a: ");
  scanf("%f", &a);
  printf("Enter a number b: ");
  scanf("%f", &b);
  printf("Enter number of breaks n: ");
  scanf("%d", &n);
  printf("Enter a number y: ");
  scanf("%f", &y);
  h = (b - a) / n;
  printf("Step h: %f\n", h);
  printf("\n x y\n\n");
  printf(" %.4f %f\n", a, y);
  for(x = a; x <= b - h; x += h)
  {
    y += h * y * (1 - x);
    printf(" %.4f %f\n", x + h, y);
  }
}

void m_rung_kutt() //метод Рунге-Кутта
{
  float a, b, y, n, h, x, f, k1, k2, k3, k4;
  printf("Runge-Kutta Method\n\n");
  printf("Enter a number a: ");
  scanf("%f", &a);
  printf("Enter a number b: ");
  scanf("%f", &b);
  printf("Enter number of breaks n: ");
  scanf("%f", &n);
  printf("Enter a number y: ");
  scanf("%f", &y);
  h = (b - a) / n;
  printf("Step h: %.4f\n", h);
  printf("\n x y\n\n");
  printf(" %.4f %f\n", a, y);
  for(x = a; x <= b - h; x += h)
  {
    k1 = h * fdy(x, y);
    k2 = h * fdy(x + h / 2, y + k1 / 2);
    k3 = h * fdy(x + h / 2, y + k2 / 2);
    k4 = h * fdy(x + h, y + k3);
    f = (k1 + 2 * k2 + 2 * k3 + k4) / 6;
    y += f;
    printf(" %.4f %f\n", x + h, y);
  }
}

void m_system_euler() //система диф. ур-ий
{
  float a, b, h, x, y, z, x1, y1, z1, t;
  printf("Differential equation system\n\n");
  printf("Enter a number a: ");
  scanf("%f", &a);
  printf("Enter a number b: ");
  scanf("%f", &b);
  printf("Enter step h: ");
  scanf("%f", &h);
  printf("Enter a number x: ");
  scanf("%f", &x);
  printf("Enter a number y: ");
  scanf("%f", &y);
  printf("Enter a number z: ");
  scanf("%f", &z);
  printf("\n t x y z\n");
  printf(" %.4f %f %f %f\n", a, x, y, z);
  for(t = a; t <= b - h; t += h)
  {
    x1 = x;
    y1 = y;
    z1 = z;
    x1 += h * (-2 * x + 5 * z);
    y1 += h * (sin(t - 1) * x - y + 3 * z);
    z1 += h * (-x + 2 * z);
    printf(" %.4f %f %f %f\n", t + h, x1, y1, z1);
    x = x1;
    y = y1;
    z = z1;
  }
}

void m_dy_second_order() //диф. ур-ия 2-ого порядка
{
  float a, b, h, x, y, z, y1;
  printf("Second order differential equations\n\n");
  printf("Enter a number a: ");
  scanf("%f", &a);
  printf("Enter a number b: ");
  scanf("%f", &b);
  printf("Enter step h: ");
  scanf("%f", &h);
  printf("Enter a number y: ");
  scanf("%f", &y);
  printf("Enter a number y': ");
  scanf("%f", &z);
  printf("Step h: %f\n", h);
  printf("\n x y z\n\n");
  printf(" %.4f %f %f\n", a, y, z);
  for(x = a; x <= b - h; x += h)
  {
    y1 = y + h * z;
    z = z - h * (z / x + y);
    y = y1;
    printf(" %.4f %f %f\n", x + h, y, z);
  }
}

void m_x_y() //y'=x+y
{
  float a, b, y, h, x;
  printf("y' = x + y\n\n");
  printf("Enter a number a: ");
  scanf("%f", &a);
  printf("Enter a number b: ");
  scanf("%f", &b);
  printf("Enter step h: ");
  scanf("%f", &h);
  printf("Enter a number y: ");
  scanf("%f", &y);
  printf("\n x y\n\n");
  printf(" %.4f %f\n", a, y);
  for(x = a; x <= b - h; x += h)
  {
    y = y + h * (x + y);
    printf(" %.4f %f\n", x + h, y);
  }
}

void menu()
{
  int meth;
  do{
    system("cls");
    printf("Main menu:\n\n");
    printf("1. Euler Method\n2. Runge-Kutta Method\n3. Differential equation system\n4. Second order differential equations\n5. y' = x + y\n6. exit\n");
    scanf("%d",&meth);
    switch (meth)
    {
      case 1:
        system("cls");
        m_eiler();
        system("pause");
        break;
      case 2:
        system("cls");
        m_rung_kutt();
        system("pause");
        break;
      case 3:
        system("cls");
        m_system_euler();
        system("pause");
        break;
      case 4:
        system("cls");
        m_dy_second_order();
        system("pause");
        break;
      case 5:
        system("cls");
        m_x_y();
        system("pause");
        break;
    }
  }while (meth != 6);
}

int main() //главная функция
{
  menu();
  return 0;
}
```
