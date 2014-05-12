/**
 * An apex page controller that exposes the site forgot password functionality
 */
public with sharing class ForgotController {
    public String username {get; set;}   
       
    public ForgotController() {}
  
    public PageReference forgotPassword() {
      boolean success = Site.forgotPassword(username);
      PageReference pr = Page.ForgotConfirm;
      pr.setRedirect(true);
      
      if (success) {        
        return pr;
      }
      return null;
    }
}