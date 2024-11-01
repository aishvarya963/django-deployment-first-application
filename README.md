# django-deployment-first-application
import mysql.connector;
conn=None;mycursor=None
try:
#update the data
    conn=mysql.connector.connect(host="localhost",user="root",
    password="root",port=3308,database="mydb")
    mycursor=conn.cursor()
    increment=int(input("Enter the increased value"))
    collrange=int(input("Enter the collection range"))
    sqlcmd="update temple set tcoll=tcoll+%s where tcoll<%s"
    mycursor.execute(sqlcmd,(increment,collrange))#tuple of values
    print("Records updated successfully",mycursor.rowcount)
#delete the data
    limit=int(input("Enter the limit amount to delete"))
    sqcd="delete from temple where tcoll<%s";
    mycursor.execute(sqcd%limit);
    print(mycursor.rowcount,"Records Deleted Succesfully")
    conn.commit()
    
except mysql.connector.DatabaseError as e:
    print("Error in executing SQL-cmds",e)
    if conn:conn.rollback();
finally:
    if mycursor:mycursor.close()
    if conn:conn.close()
