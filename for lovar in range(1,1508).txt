for lovar in range(1,1508):
    speedlist1= data.loc[data['Veh_Id'] == lovar, 'vy_smooth'].tolist()
    
    speed1=[]
    for i in speedlist1:
        if i<0:
            speed1.append(i)
        else:
            speed1.append(i)
    timelist1= data.loc[data['Veh_Id'] == lovar, 'TimeStamp'].tolist()
    widthlist= data.loc[data['Veh_Id'] == lovar, 'Width'].tolist()
    if len(widthlist)!=0:
        width=widthlist[0]
        lonpos=data.loc[data['Veh_Id'] == lovar, 'Lon_smooth'].tolist()
        maximum1=max(speed1)
        index1=speed1.index(maximum1)
        le=len(speed1)
        extend1=-1 
        extend2=-1
        for i in range(index1,le-1):
            if speed1[i]<speed1[i+1]:
                if speed1[i]<0.1:
                    extend2=i

                break
        for i in range(index1,1,-1):
            if speed1[i]<speed1[i-1]:
                if speed1[i]<0.1:
                    extend1=i
                break
        if extend1==-1 or extend2==-1:
            ans="neglected"
        else:
            longleft=lonpos[extend1]
            longright=lonpos[extend2]
            diff=abs(longleft-longright)
            if(diff>width):
                ans="yes"
            else:
                ans="no"
    print("Vehicle ID",lovar,"\n \n")
    plt.plot(timelist1,speed1)
    plt.ylabel('Lateral Speed')

    plt.xlabel('Time')

    plt.title('lateral speed vs time')
    plt.show()
    print("lane shift=", ans)
