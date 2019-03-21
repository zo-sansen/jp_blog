---
title: 空白博客
date: 2019-2-13
author: alanJiang
tags:
    - HEXO
categories:
    - 个博搭建
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: 空白博客
---

```java
class a{
     public static void main(String[] args) throws IOException {
            create(2000000,10000000);
        }
    
        /**
         * 创建数据
         * @param segment 分多少条一个文件
         * @param end 总共创建多少条
         * @throws IOException
         */
        public static void create(int segment,int end) throws IOException {
            int filename = 1;
            int seg = segment,max =end;
            int nowMax = max / seg;
            for(int i=1;i<=nowMax;i++){
                boolean isAppend = false;
                System.out.println("一个文件");
                for(int j=(seg-segment*9/10);j<=seg;j=j+(segment/10)){
                    System.out.println(j);
                    int jbMin = j - segment/10 + 1, jbMax = j;
                    System.out.println(jbMin + "\t" + jbMax);
                    isAppend = test(jbMin,jbMax,filename,isAppend);
                }
                seg +=segment;
                filename++;
            }
        }
    
        public static boolean test(int min,int max,int filename,boolean isAppend) throws IOException {
            File file = new File("/home/jp/code/parkingMicroservice/microservices/adminserver/src/main/resources/orderBig"+filename+".sql");
            File file2 = new File("/home/jp/code/parkingMicroservice/microservices/adminserver/src/main/resources/parkBig"+filename+".sql");
            StringBuilder sb = new StringBuilder(
                    "insert into order_record(id,orderno,park_id) values");
            StringBuilder sb2 = new StringBuilder(
                    "insert into parking_record(id,record_orderno,start_time,end_time,park_id) values");
            Random random = new Random();
            for(int i=min;i<=max;i++){
                if(i>min){
                    sb.append(",");
                }
                String order = System.currentTimeMillis() + (random.nextInt(1000) + 1)+"";
                int parkId = (random.nextInt(11) + 1);
                sb.append("(");
                sb.append(i);
                sb.append("," + order);
                sb.append("," + parkId);
                sb.append(")");
                if(i>min){
                    sb2.append(",");
                }
                sb2.append("(");
                sb2.append(i);
                sb2.append(","+order);
                sb2.append(",");
                sb2.append(System.currentTimeMillis()/1000 - (random.nextInt(100000) + 1));
                sb2.append("," + System.currentTimeMillis()/1000);
                sb2.append("," + parkId);
                sb2.append(")");
            }
            sb.append(";\r\n");
            sb2.append(";\r\n");
            OutputStream outputStream= new FileOutputStream(file,isAppend);
            OutputStream outputStream2= new FileOutputStream(file2,isAppend);
            outputStream.write(sb.toString().getBytes());
            outputStream2.write(sb2.toString().getBytes());
            outputStream.flush();
            outputStream2.flush();
            outputStream.close();
            outputStream2.close();
            return true;
        }
}
```



{% raw %}
<style>
qq {
     padding: 2px 4px;
     font-size: 90%;
     color: #c7254e;
     background-color: #f9f2f4;
     border-radius: 4px;
 }
</style>
{% endraw %}
