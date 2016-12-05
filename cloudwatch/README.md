# ansible

##To create cloudwatch alarms set 'alert_state' to present
ansible-playbook monitorying.yml --extra-vars "alert_state=present"

##To remove all cloudwatch alarms created set 'alert_state' to absent
ansible-playbook monitorying.yml --extra-vars "alert_state=absent"

set below listed variables in defaults variable file
-----------------------------------------------------

	aws_region : us-west-2
	alert_state : absent
	alert_prefix : team-name
	app_alarm_action :
	  - "arn:aws:sns:us-west-2:111111304611:Test_Alert"

	cpu_threshold : 75.0
	memory_threshold : 75.0
	disk_threshold : 75.0

change tasks file and set tag values according to what is set in ec2 tags
------------------------------------------------------------------------

	- name: gather ec2 istance details
	  ec2_remote_facts:
	    region: "{{ aws_region }}"
	    filters:
	      instance-state-name: running
	      "tag:team": teamname
	      "tag:environment": stg

	  register: aws_ec2_instance




