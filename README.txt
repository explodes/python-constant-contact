Note:
	Feel free to contribute patches for more functionality, the only methods I added were ones I needed for my own project. I also appended a django project to keep track of nightly batch jobs instead of calling the api during normal web processing.

Overview:
	Python wrapper for constantcontacts developer API.

Usage:
	from python_constantcontact import cc
	
	api = cc.Api(api_key="some-api-key-123", username="someusername", password="123")
	
	# should return a 201 CREATED response status code
	response, body = api.create_contact("joeschmoe123@gmail.com", [2,3])
	response, body = api.create_contact("marysmith@gmail.com", [1], first_name="mary", last_name="smith")

	# these will both return the same xml body; get contact by email is just a convenience method 
	# if we don't have the id (common case)
	id, xmlbody = api.get_contact_by_email(marysmith@gmail.com)
	xmlbody = api.get_contact_by_id(id)

	# again, email is just a convenience method since I imagine most people don't store the CC id
	# should return a 204 UPDATED response status code
	response, body = api.add_contact_to_lists_by_email("joeschmoe123@gmail.com", [1])
	response, body = api.add_contact_to_lists_by_id(id, [2,3])

	# removes the contact from all mailing lists, this does NOT use the do-not-mail 
	# feature of CC, it literally removes the contact from all lists
	# should return a 204 UPDATED response status code
	response, body = api.remove_contact_by_email("joeschmoe123@gmail.com")
	response, body = api.remove_contact_by_id(id)