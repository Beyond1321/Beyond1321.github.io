---
layout: post
title: GET the date list between two timestamps
categories: java
typora-root-url: ..
tags: [java,misc]
---

example:

​	input: timestamp1, timestamp2

​	output: [20220101,20220102...]

## Get time by timestamp

We usually get the timestamp in the form of UNIX which is accurate to seconds. In java, the timestamp is accurate to milliseconds.

```java
	public static String getTimeByTimestamp(int time){
        long timeStamp = (long) time *1000;
        SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        return sdf.format(new Date(timeStamp));
    }
```

## Get timestamp by time

```java
public static String getTimestampByTime(String s) throws ParseException {
    String res;
    SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
    Date date = simpleDateFormat.parse(s);
    long ts = date.getTime();
    res = String.valueOf(ts);
    return res;
}
```

## Get the days list with two timestamps

```java
	public static List<String> getDaysList(int time1,int time2) throws ParseException {
        List<String> list = new ArrayList<>();
        String date1 = getTimeByTimestamp(time1).substring(0,10);
        String date2 = getTimeByTimestamp(time2).substring(0,10);
        int days = getDaysBetweenTwoDates(date1,date2);
        Date start = new Date(((long) time1)*1000);
        Calendar cal=new GregorianCalendar();
        cal.setTime(start);
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyyMMdd");
        for(int i=0;i<days-1;i++){
            cal.add(Calendar.DATE,1);
            list.add(simpleDateFormat.format(cal.getTime()));
        }
        if(days!=0){
            list.add(date2.substring(0,4)+date2.substring(5,7)+date2.substring(8,10));
        }

        for (String s : list) {
            System.out.println(s);
        }
        return list;
    }

	public static int getDaysBetweenTwoDates(String dateStr1, String dateStr2) {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyyMMdd");
        SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy-MM-dd");
        try {
            dateStr1 = sdf.format(sdf2.parse(dateStr1));
            dateStr2 = sdf.format(sdf2.parse(dateStr2));
        } catch (ParseException e) {
            e.printStackTrace();
        }
        int year1 = Integer.parseInt(dateStr1.substring(0, 4));
        int month1 = Integer.parseInt(dateStr1.substring(4, 6));
        int day1 = Integer.parseInt(dateStr1.substring(6, 8));
        int year2 = Integer.parseInt(dateStr2.substring(0, 4));
        int month2 = Integer.parseInt(dateStr2.substring(4, 6));
        int day2 = Integer.parseInt(dateStr2.substring(6, 8));
        Calendar c1 = Calendar.getInstance();
        c1.set(Calendar.YEAR, year1);
        c1.set(Calendar.MONTH, month1);
        c1.set(Calendar.DAY_OF_MONTH, day1);
        Calendar c2 = Calendar.getInstance();
        c2.set(Calendar.YEAR, year2);
        c2.set(Calendar.MONTH, month2);
        c2.set(Calendar.DAY_OF_MONTH, day2);
        long mills =
                c1.getTimeInMillis() > c2.getTimeInMillis()
                        ? c1.getTimeInMillis() - c2.getTimeInMillis()
                        : c2.getTimeInMillis() - c1.getTimeInMillis();
        return (int) (mills / 1000 / 3600 / 24);
    }
```