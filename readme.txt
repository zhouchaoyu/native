Java ���ñ��ش���֮native
h3.

������ 

     Java�����е�native�ؼ��֣��Լ�Java���Ե���C���Եı������ɱ��ض�̬���ӿ�(DLL)ʾ���� 
     һ. ʲô��JNI
����JNI��Java Native Interface����д�����ṩ�����ɵ�APIʵ����Java���������Ե�ͨ�ţ���Ҫ��C&C++������Java1.1��ʼ��JNI��׼��Ϊjavaƽ̨��һ���֣�������Java�������������д�Ĵ�����н�����JNIһ��ʼ��Ϊ�˱����ѱ������ԣ�������C��C++����Ƶģ�����������������ʹ������������ԣ�ֻҪ����Լ����֧�־Ϳ����ˡ�ʹ��java�뱾���ѱ���Ĵ��뽻����ͨ����ɥʧƽ̨����ֲ�ԡ����ǣ���Щ������������ǿ��Խ��ܵģ������Ǳ���ġ����磬ʹ��һЩ�ɵĿ⣬��Ӳ��������ϵͳ���н���������Ϊ����߳�������ܡ�JNI��׼����Ҫ��֤���ش����ܹ������κ�Java ����������¡�

�����ܵ���˵��JNI����һ������Java���Ժ������������(��Ҫ��C/C++)ͨ�ŵĽӿڡ�C/C++��ϵͳ���ı������, �������������κκ�ϵͳ��صĳ�������, ����Java�����д�ײ��Ӧ�ñȽ���ʵ��, ʹ��JNI���Ե������еı��ؿ�, ����������Java�Ŀ���. C/C++��Ч����Ŀǰ��õ�����, ����ʹ��C/C++��ʵ��һЩʵʱ�Էǳ��ߵĲ���. C/C++��Java�����Ƿǳ����еı������, һЩ��������о���ʹ������֮��Ļ�ϱ��.

����һ��ʹ��JNI, JAVA�����ɥʧ��JAVAƽ̨�������ŵ�: �����ڿ�ƽ̨��Ҫ���ƽ̨�������ڲ�ͬ��ϵͳ���������±��뱾�����Բ��֣��������Ǿ��԰�ȫ�ģ����ش���Ĳ���ʹ�ÿ��ܵ����������������һ��ͨ�õĹ����ǣ���Ӧ���ñ��ط������������������൱�У������ͽ�����Java���Ժ�C/C++֮�������ԡ�

����ʹ��JNIʵ��Java��C���Ի�ϱ�̵Ļ����������£�

       1. ��д����native�����ķ�����java��
       2.ʹ��javac����������е�java��
       3.Ȼ��ʹ��javah + ����������չ��Ϊ.h��ͷ�ļ�
       4.ʹ��C/C++ʵ�ֱ��ط���
       5.��C/C++��д���ļ����ɶ�̬���ӿ�
       6. java���ش����ӿ� 

����ʾ���� 

         ��һ����д��java native ����
          public class NativeMethod {

     public static void main(String[] args)
        { 

            System.loadLibrary("Tool"); 
            NativeMethodLoader nmt = new NativeMethodLoader();
            Double double1 = Double.valueOf(args[0]);
            Double double2 = Double.valueOf(args[1]);
            System.out.println(double1+"----------------"+double2);
            double add = nmt.Add(double1,double2);
            System.out.println(add);

        }

    static class NativeMethodLoader
    {   
       public native double Add(double x,double y);
    }

}
        2.����java ����class�ļ�       
        3. ����.h�ļ�
        ������������������
        4. ʵ�ֵײ��������dll���ӿ�
        5. ��dll������classpath��

�༭������
���н����

      C:\Users\mayn\Desktop\nativeMethod>java NativeMethod 8 9
8.0----------------9.0
17.0

C:\Users\mayn\Desktop\nativeMethod>java NativeMethod 100000 9999
100000.0----------------9999.0
109999.0

C:\Users\mayn\Desktop\nativeMethod>java NativeMethod 1000000000000000000 9999
1.0E18----------------9999.0
1.00000000000000998E18

C:\Users\mayn\Desktop\nativeMethod>