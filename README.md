# hotel-management-system-python-class-12
import mysql.connector
mydb= mysql.connector.connect(user='Prathmesh', password='password', host='localhost', database='hotel')
mycur= mydb.cursor()
def registercus():
    L=[]
    r=[]
    s = input('enter S.No.:')
    L.append(s)
    name= input('enter customer name:')
    L.append(name)
    chkin= input('enter checkin date(dd/mm/yyyy):')
    L.append(chkin)
    chkout= input('enter checkout date(dd/mm/yyyy):')
    L.append(chkout)
    id= input('please enter your identity no:')
    L.append(id)
    room= input('enter room number:')
    L.append(room)
    r.append(room)
    paid= input('enter amount paid')
    L.append(paid)
    unpaid= input('enter amount left')
    L.append(unpaid)
    sql='insert into cus_data(s_no,cus_name, checkin, checkout, id_no, room_no, amount_paid, amount_left) values(%s,%s,%s,%s,%s,%s,%s,%s)'
    mycur.execute(sql,L)
    sql1="update roomavailable set status= 'occupied' where roomno = %s"
    mycur.execute(sql1,r)
    mydb.commit()

def viewrooms():
 a='select * from rooms'
 mycur.execute(a)
 rows= mycur.fetchall()
 for i in rows:
  print(i)   

def viewbill():
    l=[]
    h=[]
    p=input('enter room no.:')
    h.append(p)
    b='select cus_name, amount_paid, amount_left from cus_data where id_no = %s'
    idn=int(input('enter id no:'))
    l.append(idn)
    mycur.execute(b,l)
    rows= mycur.fetchall()
    for c in rows:
        print(c)
    w=rows[0]
    print(w[2],'has to be paid by the customer')
    sql2="update roomavailable set status= 'vacant' where roomno = %s"
    mycur.execute(sql2,h)
    mydb.commit()
def viewroomsavailable():
    z="select * from roomavailable where status= 'vacant'"
    mycur.execute(z)
    gg= mycur.fetchall()
    for w in gg:
        print(w)

def restaurent():

  z="select * from restaurent"
  mycur.execute(z)
  gg= mycur.fetchall()
  for w in gg:
    print(w)

  l=[]
  s= input('customer name:')
  l.append(s)
  
  b= int(input('enter item_no:'))
  q= int(input('enter quantity'))
  if b==1:
     iname='tea'
     r=20*q
     l.append(iname)
     l.append(q)
     l.append(20)
     l.append(r)
     print('pay rupees', r, 'for', iname)   
  elif b== 2:
     iname= 'coffee'
     r=30*q
     l.append(iname)
     l.append(q)
     l.append(30)
     l.append(r)
     print('pay rupees', r, 'for', iname) 
  elif b== 3:
     iname= 'burger'
     r=120*q
     l.append(iname)
     l.append(q)
     l.append(120)
     l.append(r)
     print('pay rupees', r, 'for', iname)  
  elif b== 4:
     iname= 'popcorn'
     r=50*q
     l.append(iname)
     l.append(q)
     l.append(50)
     l.append(r)
     print('pay rupees', r, 'for', iname)  
  elif b== 5:
     iname= 'pizza'
     r=200*q
     l.append(iname)
     l.append(q)
     l.append(200)
     l.append(r)
     print('pay rupees', r, 'for', iname)  
  elif b== 6:
     iname= 'mineral water'
     r=20*q
     l.append(iname)
     l.append(q)
     l.append(20)
     l.append(r)
     print('pay rupees', r, 'for', iname)  
  else:
     print('wrong input')
  z='insert into food_order(cus_name, item_name, quantity, rate, tprice) values (%s,%s,%s,%s,%s)'
  mycur.execute(z,l)
  mydb.commit()     


j= input('want to run the hotel management system?(y/n):')
while j=='y' or j=='Y':
 print('''1- Check in
2- view rooms
3- Check Out
4- view available rooms
5- restaurent menu''')
 ch=int(input('enter your choice'))
 if ch== 1:
   registercus()
   j= input('want to run the hotel management system?(y/n):')
   print('''



''')
 elif ch== 2:
    viewrooms()
    j= input('want to run the hotel management system?(y/n):')
    print('''



''')
    
 elif ch== 3:
    viewbill()
    j= input('want to run the hotel management system?(y/n):')
    print('''



''')
 elif ch== 4:
    viewroomsavailable()
    j= input('want to run the hotel management system?(y/n):')
    print('''



''')
 elif ch== 5:
    restaurent()
    j= input('want to run the hotel management system?(y/n):')
    print('''



''')
 else:
    print('inappropriate input')
    j= input('want to run the hotel management system?(y/n):')
