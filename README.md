# Django app for i18n support in edx xblocks

# ISSUES 
* It looks like it does not work with the `drag and drop v2` xblock since that
  xblock already has an internal translation service - which is not working.
  [See this](https://github.com/libremente/xblock-drag-and-drop-v2#i18n-compatibility)

# HOW TO
1. Install the app
    * Clone the repo locally
    * `pip install -e <path_to_cloned_folder>`
    * Check with `pip freeze | grep django-xblock-i18n` that the module is properly
      installed 
    * Add the app to the `INSTALLED_APPS` in Django. This can be done in  
      edx in `lms/envs/common.py` in the `INSTALLED_APPS` section: 

      ```
      # xblocks_i18n 
      # see this: https://github.com/eduNEXT/django-xblock-i18n
      'xblock_i18n',
      ```
2. Add the service 

    Add the service to the context in the xblock's main `<xblock_name>.py`
    file in order to load the
    service properly. For example in the `poll` xblock this can be done
    by inserting in the `poll.py` file in the `student_view` method
    of the `PollBlock` Class
    the following code:

    ```
    # Adding i18 service in the context
    context["i18n_service"] = self.runtime.service(self, "i18n")
    ``` 

    or directly in the `context.update` array:
    
    ```
    "i18n_service" : self.runtime.service(self, "i18n"),
    ```

3. Load the tag in the template

    Add the `{% load xblock_i18n %}` at the top of the template file. 
    Be sure that the translatable strings are sourrounded by a `trans` block like
    e.g. `{% trans "string_to_be_localized" %}`

4. See
   [this](https://github.com/libremente/xblock-poll/commit/a3f5564e6b93855602080a3da0489062a0cb127a) 
   commit for more reference. 


# Credits (todo)
Originally created by Felipe Montoya
