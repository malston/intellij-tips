Deploying exploded war with Tomcat in Intellij
This cannot be done if you deploy a war with IntelliJ IDEA. However, it can be if you deploy an exploded war. In IDEA:
1. open your Tomcat Run/Debug configuration (Run > Edit Configurations)
2. Go to the "Deployment" tab
3. In the "Deploy at Server Startup" section, remove (if present) the artifact my-webapp-name:war
4. Click the add icon, select 'artifact' and then select my-webapp-name:war exploded
5. Click OK (on the "Select Artifacts to Deploy" dialog)
6. Still in the Run/Debug Configuration Window, select the "Server" tab
7. In the middle of that tab, change the "On frame Deactivation" setting to either "Update resources" or "Update Classes and Resources"
    * _Update resources:_ All changed resources (that is, all application components other than the classes) will be updated.
    * _Update classes:_ and resources. All changed resources will be updated; changed classes will be recompiled. Note that whether the actual classes will be updated depends on the capabilities web server. If I recall, Tomcat will reload html/xhtml and jsp files, but not Servlets or classes that JSPs or Servlets use. You need to modified Tomcat to use a dynamic classloader for that.
8. You can also set the "On 'update'" action as well.
    * This determined what happens when you hit the Update icon (or Ctrl+F10) in the Run window.
    * the "Show dialog" determines if IDEA prompts you each time you hit the update icon
9. Click OK.
Now anytime you make a change, IDEA will redeploy the changed file(s) when IDEA's frame is deactivated (i.e. loses focus). It does take a second or two, You'll see it in the lower status bar in IDEA. Obviously. you'll still need to refresh your web browser so it fetches the new file (unless of course if the page has an auto refresh of ajax like fetch).
A good combination with Tomcat is to set "On frame deactivation" to "Update Resources" and the "On 'update'" action to either "Redeploy" or "Restart Server". That allows static pages to be quickly updated via frame deactivation, and class updated via the 'update' action.
