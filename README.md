package com.company;

import java.util.Arrays;
import java.util.Scanner;
import java.util.ArrayList;
import java.util.List;
import java.lang.String;

public class Module_4 {
    public static void main(String[] args) {
        System.out.println("Задача №1.");
        Task1();
        System.out.println("Задача №2.");
        Task2();
         System.out.println("Задача №3.");
        Task3();
        System.out.println("Задача №4.");
        Task4();
       System.out.println("Задача №5.");
        Task5();
        System.out.println("Задача №6.");
        Task6();
        System.out.println("Задача №7.");
        Task7();
        System.out.println("Задача №8.");
        Task8();
       System.out.println("Задача №9. ");
        Task9();
        System.out.println("Задача №10.");
        Task10();
    }

    //Задача 1. Эссе, не более к символов в строке
    public static void Task1(){
        Scanner scanstr = new Scanner(System.in);
        System.out.println("Enter variables: ");
        int n = scanstr.nextInt();
        int k = scanstr.nextInt();
        System.out.println("Enter essay: ");
        Scanner scantxt = new Scanner(System.in);
        String text = scantxt.nextLine();
        System.out.println("Your essay: ");

        int ks = 0;
        int kolp = 0;
        int current = 0;
        int last = 0;
        while (current != -1) {

            while (ks <= k) {
                int position = text.indexOf(" ", current + 1);
                kolp += 1;
                current = position;
                int next = text.indexOf(" ", current + 1);
                if (next != -1) {
                    ks = next - kolp - last;
                }
                else {
                    ks = 1000;
                }
            }

            if (ks != 1000) {
                int start = last;
                int end = current;
                char[] dst = new char[end - start];
                text.getChars(start, end, dst, 0);
                System.out.println(dst);
                last = current + 1;

                ks = 0;
                kolp = 0;
            }
            else {
                int start = last;
                int end = current;
                char[] dst = new char[end - start];
                text.getChars(start, end, dst, 0);
                System.out.println(dst);
                last = current + 1;

                start = last;
                end = text.length();
                char[] nst = new char[end - start];
                text.getChars(start, end, nst, 0);
                System.out.println(nst);
                current = -1;
            }
        }
    }

    //Задача 2. Класер скобок
    public static void Task2(){
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the line");
        String s = sc.nextLine();
        System.out.println("Answer: " + Arrays.toString(Split(s)));
    }
    public static String[] Split(String s){
        List<String> list = new ArrayList<String>();
        int f = 0;
        int i = 0;
        while (s.length() > 0) {
            if (s.charAt(i) == '(') f++;
            else f--;
            if (f == 0) {
                list.add(s.substring(0, i + 1));
                s = s.substring(i + 1);
                i = 0;
                continue;
            }
            i++;
        }
        return list.toArray(new String[list.size()]);
    }

    //Задача 3. Изменить стиль написанпия строки по заданным правилам
    public static void Task3(){
        System.out.println("Enter string to CamelCase: ");
        Scanner scantxt = new Scanner(System.in);
        String text = scantxt.nextLine();
        System.out.println("toCamelCase: " + toCamelCase(text));

        System.out.println("Enter string to SnakeCase: ");
        Scanner scanstr = new Scanner(System.in);
        String str = scanstr.nextLine();
        System.out.println("toSnakeCase: " + toSnakeCase(str));
    }

    public static String toCamelCase(String str){
        int position = 0;
        while (position != -1){
            position = str.indexOf("_");
            if(position != -1) {
                str = str.substring(0, position) + str.substring(position + 1,position + 2).toUpperCase() + str.substring(position + 2);
            }
        }

        return str;
    }

    public static String toSnakeCase(String str){
        int i = 0;
        while (i != str.length()){
           char ch = str.charAt(i);
            if (Character.isUpperCase(ch)){
                str = str.substring(0,i) + "_" + str.substring(i, i + 1).toLowerCase() + str.substring(i + 1);
            }
            i++;
        }
        return str;
    }

    //Задача 4. Оплата по часам работы
    public static void Task4(){
        Scanner scanstr = new Scanner(System.in);
        //вводим данные первого массива
        int length = 4;
         double [] arr = new double[length];
        System.out.println("Enter the elements of the array:");

        for(int i=0; i<length; i++ ) {
            arr[i] = scanstr.nextDouble();
        }

        System.out.println("The result is: $" + overTime(arr));
    }

    public static String overTime(double[] arr){
        double sum = 0;
        if (arr[1] > 17){
            double under = arr[1] - 17;
            sum = (17 - arr[0]) * arr[2] + under * arr[2] * arr[3];
        }
        else {
            sum = (arr[1] - arr[0]) * arr[2] ;
        }
        String result = String.format("%.2f",sum);
        return result;
    }

    //Задача 5. Индекс массы тела
    public static void Task5(){
        Scanner scanstr = new Scanner(System.in);
        System.out.println("Enter your weight: ");
        String weight = scanstr.nextLine();
        System.out.println("Enter your height: ");
        String height = scanstr.nextLine();
        System.out.println("The result is: " + BMI(weight, height));
    }

    public static String BMI(String weight, String height){
        double ves = 0;
        double rost = 0;
        String itog = "";
        int position = weight.indexOf(" ");
        String wes = weight.substring(0,position);
            ves = Double.parseDouble(wes);
        String kilopound = weight.substring(position+1);

        position = height.indexOf(" ");
        String ros = height.substring(0,position);
            rost = Double.parseDouble(ros);
        String metrinch = height.substring(position+1);

        if (kilopound.equals("pounds")){
            ves = ves * 0.453592;
        }
        if (metrinch.equals("inches")){
            rost = rost * 0.0254;
        }

        double IMT = ves/(rost*rost);

        if (IMT < 18.5){
           itog = " Underweight";
        }
        if ((IMT >= 18.5)&&(IMT<=24.9)){
            itog = " Normal weight";
        }
        if (IMT > 24.9){
            itog = " Overweight";
        }

        String result = String.format("%.1f",IMT) + itog;

        return result;
    }

    //Задача 6. Мультипликативное постоянство, т.е. количество раз, которое нужно умножать цифры в числе, пока не останется одна цифра.
    public static void Task6(){
        Scanner scanstr = new Scanner(System.in);
        System.out.println("Enter number: ");
        int num = scanstr.nextInt();
        System.out.println("The result is: " + bugger(num));
    }

    public static int bugger(int num){
        int k = 0;
        while (num/10 != 0){
            int mod = 1;
           while (num != 0){
               mod = mod * (num % 10);
               num = num / 10;
           }
           num = mod;
           k++;
        }
        return k;
    }

    //Задача 7. Если символ повторяется n раз, преобразуйте его в символ*n.
    public static void Task7() {
        System.out.println("Enter string: ");
        Scanner scantxt = new Scanner(System.in);
        String text = scantxt.nextLine();
        System.out.println("The result is: " + toStarShorthand(text));
    }

    public static String toStarShorthand(String text){

        int k = 0;
        int i = 1;
        while (i != text.length()){
            if (text.charAt(i) == text.charAt(i-1)){
                k++;
            }
            else{
                if (k != 0){
                    text = text.substring(0,i-k) + "*" + (k+1) + text.substring(i);
                    k = 0;
                }
            }
            i++;
        }
        if (k != 0){
            text = text.substring(0,i-k) + "*" + (k+1) + text.substring(i);
            k = 0;
        }
        return text;
    }

    //Задача 8. Рифмуются ли строки
    public static void Task8(){
        System.out.println("Enter the first string: ");
        Scanner scantxt = new Scanner(System.in);
        String text = scantxt.nextLine();
        System.out.println("Enter the second string: ");
        Scanner scanstr = new Scanner(System.in);
        String str = scanstr.nextLine();
        System.out.println("Do these lines rhyme? " + doesRhyme(text,str));
    }

    public static boolean doesRhyme(String first, String second){
        first = first.trim();
        second = second.trim();
        String FlastWord = first.substring(first.lastIndexOf(" ")+1);
        String SlastWord = second.substring(second.lastIndexOf(" ")+1);
        //System.out.println(FlastWord);
       // System.out.println(SlastWord);

        String str1 = "";
        String str2 = "";

        for (int j = 0; j < FlastWord.length(); j++) {
            switch (FlastWord.charAt(j)) {
                case 'a': case 'e': case 'i': case 'o': case 'u': case 'y':
                case 'A': case 'E': case 'I': case 'O': case 'U': case 'Y':
                    str1 += String.valueOf(FlastWord.charAt(j));
            }
        }

        for (int i = 0; i < SlastWord.length(); i++) {
            switch (SlastWord.charAt(i)) {
                case 'a': case 'e': case 'i': case 'o': case 'u': case 'y':
                case 'A': case 'E': case 'I': case 'O': case 'U': case 'Y':
                    str2 += String.valueOf(SlastWord.charAt(i));
            }
        }

       // System.out.println(str1);
      //  System.out.println(str2);
         return (str1.equalsIgnoreCase(str2));
    }

    //Задача 9. Если в 1 числе 3 цифры подряд, а во втором 2 такие же подряд
    public static void Task9(){
        Scanner scanstr = new Scanner(System.in);
        System.out.println("Enter the first number: ");
        String num1 = scanstr.nextLine();
        System.out.println("Enter the second number: ");
        String num2 = scanstr.nextLine();
        System.out.println("The result is: " + trouble(num1, num2));
    }

    public static boolean trouble(String str1, String str2) {
        boolean res = false;
        int k1 = 0;
        int k2 = 0;
        char new1[]=str1.toCharArray();
        char new2[]=str2.toCharArray();

        int i = 1;
       while (i != str1.length()) {
            if (new1[i] == new1[i-1]) {
                k1++;
            }
            else{
                if (k1 == 2){
                    int j = 1;
                    while (j != str2.length()) {
                        if (new2[j] == new2[j-1]) {
                            k2++;
                        }
                        else{
                            if ((k2 == 1)&&(new1[i-1] == new2[j-1])){
                               res = true;
                            }
                            k2 = 0;
                        }
                        j++;
                    }
                    if ((k2 == 1)&&(new1[i-1] == new2[j-1])){
                        res = true;
                    }
                }
                k1 = 0;
            }
            i++;
        }
        if (k1 == 2){
            int j = 1;
            while (j != str2.length()) {
                if (new2[j] == new2[j-1]) {
                    k2++;
                }
                else{
                    if ((k2 == 1)&&(new1[i-1] == new2[j-1])){
                        res = true;
                    }
                    k2 = 0;
                }
                j++;
            }
            if ((k2 == 1)&&(new1[i-1] == new2[j-1])){
                res = true;
            }
        }

       return res;
    }

    //Задача 10. Книги, концы, вхождения
    public static void Task10(){
        Scanner scanstr = new Scanner(System.in);
        System.out.println("Enter the first line: ");
        String str1 = scanstr.nextLine();
        System.out.println("Enter the second line: ");
        String str2 = scanstr.nextLine();
        System.out.println("The result is: " + countUniqueBooks(str1, str2));
    }

    public static int countUniqueBooks(String str1, String str2){
        String s = "";
        int count = 0;
        int index = 0;
        for (int i = 0; i < str1.length(); i++){
            if (str1.charAt(i) == str2.charAt(0)){
                count++;
            }
        }
        for (int j = 0; j < count/2; j++){
            index = str1.indexOf(str2, index);
            int next = str1.indexOf(str2, index + 1);
            s += str1.substring(index + 1, next);
            index = next + 1;
        }
        count = 0;
        boolean[] bool = new boolean[Character.MAX_VALUE];
        for (int x = 0; x < s.length(); x++){
            bool[s.charAt(x)] = true;
        }
        for (int y = 0; y < bool.length; y++){
            if (bool[y]){
                count++;
            }
        }

            return count;

    }

}
