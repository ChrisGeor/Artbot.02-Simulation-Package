#!/usr/bin/env python

import rospy
from geometry_msgs.msg import Twist
from sensor_msgs.msg import LaserScan



def data_provider():
	
	rospy.init_node('motion_planner',anonymous=True)
	rospy.Subscriber("/scan",LaserScan,callback)
	rospy.spin()

def callback(SensorData):
	
	motion_activator=rospy.Publisher('/cmd_vel',Twist,queue_size=100)
	motion_activator_msg=Twist()
	rate=rospy.Rate(100)
	
	flag= False
	counter=0
	for m in range (100,300):
		if(SensorData.ranges[m]>4):
			counter=counter+1
	if (counter<180):

		for i in range (100,300):
			if(SensorData.ranges[i]<4):
				flag=True
				break
		if(flag==True):
			counter1=0
			counter2=0
			for j in range (1,200):
                		if(SensorData.ranges[j]<3):
					counter1=counter1+1
			for k in range (200,400):
				if(SensorData.ranges[k]<3):
					counter2=counter2+1	
			if (counter1>counter2):	
				motion_activator_msg.linear.x= 8
               			motion_activator_msg.angular.z= 8
			elif (counter1<counter2):
				motion_activator_msg.linear.x= 8
	                	motion_activator_msg.angular.z= -8
			else:
				motion_activator_msg.angular.z=0
				motion_activator_msg.linear.x=20
	
		else:
			motion_activator_msg.linear.x=20
			motion_activator_msg.angular.z=0
	else:		
		motion_activator_msg.linear.x=20
		motion_activator_msg.angular.z=0	
		
		
			

	motion_activator.publish(motion_activator_msg)
	rate.sleep()
	
if __name__ == '__main__':
	try:data_provider()
	except rospy.ROSInterruptException: pass
			
		
		
				
