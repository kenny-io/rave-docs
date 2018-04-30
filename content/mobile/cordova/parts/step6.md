## Step 6: Configure Rave Payment

To configure the Rave payment, navigate to your terminal and run


    # ~/Desktop/Cordova-Rave/hello
    
    $ cd node_modules/cordova-rave && npm start 
    

 and hit enter on your keyboard and it’ll start running the config. 
 

![](https://d2mxuefqeaa7sj.cloudfront.net/s_D240AF2A5C6E906EAC4E921F513B0833307F0A58F2FF45FD0E64DA52C21755C0_1522853646080_CordovaNpmStart.jpg)


Note:  After the above process you will be prompted for your Rave payment public key and other required fields:


    PBFPubKey:  FLWPUBK-20795b3bfe02a5af632c8901d90e7591-X
    amount:  100
    customer_email:  roguestars2@gmail.com
    currency:  NGN
    country:  NG
    custom_title:
    custom_description:
    redirect_url:  https://www.google.com
    custom_logo:
    liveMode:  No



> Note: These are exemplary data, while setting up your project, you’ll have to use the appropriate data provided on your Rave dashboard.

When you are done answering all prompts,  run the build command and wait for the build to execute.


![](https://d2mxuefqeaa7sj.cloudfront.net/s_D240AF2A5C6E906EAC4E921F513B0833307F0A58F2FF45FD0E64DA52C21755C0_1522853632942_CordovarunBuild.jpg)


 
This will create a  `rave.js`  file in your `www` directory. Link to this file in your root index.html file. Should you modify your  `config.json`  at anytime, you will need to run the build again.

Next, in your code editor, open your project folder and navigate to the  `index.html`  file, open the file and modify it to add a pay button that will launch Rave’s pay modal.