<p align="left">
  <img src="/img/logo.png" height="150"></img>
</p>

# grID: eID for Feature Phones

<img align="right" src="/img/login.png" width="90">
<!--<i>The login screen of the eID portal as seen from a Nokia 3510 (released March 2002).</i>-->



It is common for modern eID platforms to expose their functionality through smartphone apps and Web 2.0 websites. While these interfaces may cover a large percentage of the population (depending on the demographics of each area), various groups may not have access to modern devices (e.g., smartphones). As a result, groups who have access to fewer resources may be practically excluded from using the system. To alleviate this limitation of eID systems, we introduce grID.

grID makes modern eID services accessible to feature phone users. 

grID makes use of the GPRS/WAP capabilities that even very old feature phones provide. In particular, one of the first phones to come with a WAP browser was Nokia 7110, released in October 1999. Besides a WAP browser and a connection to the network, grID does not have any other deployment of use requirements, thus making it easy to incorporate into existing eID deployments.

**This is a prototype. Do not use in production.**


## eID & Services


Our prototype supports various forms of ID and several ID-based services. For example:

* **ID**
  * Full ID (verifiable through QR code)
  * Privacy-preserving Age verification (verifiable through QR code)
  * Privacy-preserving Status verification (verifiable through QR code)
* **Health Records**
  * Vaccination Records (verifiable through QR code)
* **Local services**
  * Mail devivery notification
* **Data Management**
  * User Data Update Request
  * Display User Data

</br></br>
In cases, where the user wants to retrieve information on their own records (e.g., health records), the data are displayed as readable text. Otherwise, if the user wants to prove to a third party their identity or a certain attribute (e.g., veteran status), the "proofs" (not to be confused with cryptographic proofs) are displayed as QR codes to be scanned by the "verifier".
</br></br>


## User Interface

We now present some of the user screen that show the functionality exposed to the user:

<div>
<img align="left" src="/img/mainmenu.png" height="120">
</br>
Upon loging in, the user gains access to the main menu that displays the different categories of services available.
</br></br></br>
</div>
</br></br>

<div>
<img align="left" src="/img/idmenu.png" height="120">
</br>
The ID menu includes the different types of proof of ID that the user can use to prove their identity or attributes (optionaly in a privacy-preserving manner).
</br></br></br>
</div>
</br></br>

<div>
<img align="left" src="/img/fullid.png" height="120">
The `Full ID` option displays a single-use QR code that can be scanned by any QR code scanning app (e.g., https://play.google.com/store/apps/details?id=com.gamma.scan). Upon scanning the QR code, the app will load the URL encoded in the QR code and display the user's details. In a similar manner, in privacy-preserving proofs, the ID loaded by the QR code app, displays only certain attributes of the user e.g., to prove an age of 18+ the page includes the user's photo and a notice that the user is above 18+.
</div>
</br></br>

<div>
<img align="left" src="/img/vaccine1.png" height="120">
</br>
The user can request access to their health records (e.g., vaccination records).
</br></br></br>
</div>
</br></br>

<div>
<img align="left" src="/img/vaccine2.png" height="120">
In case, their want to prove to a third-party that they have been vaccinated they can display the corresponding QR code. In this example, the QR code is compatible with the Health Scanner App (https://play.google.com/store/apps/details?id=ie.healthpassportireland.guardian&hl=en&gl=US) used by a "verifier" to check the user's vaccination records. Overall, grID can be easily extended to support various kinds of third party apps.
</br>
</div>
</br></br>

<div>
<img align="left" src="/img/info.png" height="120">
</br></br></br></br>
</div>
</br></br>


## Deployment
To deploy the prototype, simply upload the files (maintaining the directory structure) to your own server, and load `wap.wml` on your phone's browser. It works out of the box with Apache2 but consider including rules for proper handling of wml, wmls and wbmp files.

As noted above, this is a prototype and thus far from production-ready. Some security issues that need to be taken care of before deploying it in production (besides the 'standard' php exploitation flaws etc): Ensure (on the proof verifier end) that the URL encoded in the QR code points to the trusted digital ID service provider, otherwise ignore the URL. Moreover, the current version does not perform a proper login and should be instead hooked on whatever authentication service is used. Note that captchas can be easily recreated with wbmp for feature-phones. Ensure that the URLs leading to identity proofs can be used only once to avoid replay attacks (enforced on the server side). Consequently, the URL should not point to the `wbmp` but rather to a php script that generates the QR code wbmp on-the-fly (i.e., check that the user is logged in, generate the proof, and embed the URL to the proof in the QR code) and returns it to the users browser.

The technical requirements are outlined here: https://github.com/alan-turing-institute/grID/blob/main/tech_requirements.pdf

## Acknowledgements

This work was supported, in whole or in part, by the Bill & Melinda Gates Foundation [INV-001309].

