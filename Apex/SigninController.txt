/**
 * An apex page controller that exposes the site login functionality
 */
global with sharing class SigninController {
    global String username {get; set;}
    global String password {get; set;}
    public String orgId {get; set;}
    public String siteURL  {get; set;}
    public String startURL {get; set;}
    public List<AuthProvider> authProviders {get;set;}
    
    global SigninController () {
        orgId = UserInfo.getOrganizationId();
        siteURL  = Site.getCurrentSiteUrl();
        startURL = System.currentPageReference().getParameters().get('startURL');
        if (startURL == null) startURL = '/';
        authProviders = [SELECT Id,DeveloperName,FriendlyName,ProviderType FROM AuthProvider];
    }

    global PageReference login() {
        return Site.login(username, password, startUrl);
    }
    
    global String getEncodedSiteUrl() {
        return EncodingUtil.urlEncode(siteURL, 'UTF-8');
    }
    
    global String getEncodedStartUrl() {
        return EncodingUtil.urlEncode(startURL, 'UTF-8');
    }
    
}