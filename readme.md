
* [Fork this code](https://github.com/365SI/iCSR#fork-destination-box) for learning and contribution purposes, I am open for **all** suggestions.

![](https://365csi.nl/iCSR/ipcountlogo/index.php) ![](http://365csi.nl/iCSR/images/iCSR_123.png)

### iCSR.js : A framework/support library for writing **less** JavaScript code

##### Customized Views like:

![](http://i.imgur.com/ZUNgWGh.jpg)

##### Can be created with one **iCSR.Me** statement:

```javascript
            SPClientTemplates.TemplateManager.RegisterTemplateOverrides({
            Templates: {
                Fields: {
                  "Priority":{
                    View : iCSR.Me  // <-- one iCSR statement in standard SharePoint CSR code
                  }
            };
```
##### or customized further with:

```javascript
            View : iCSR.Me({
                            colors: ['red','yellow','green'],
                            style : '<span>[svgcircle(20)]</span>'
                        })
```

![](http://i.imgur.com/pOMU6YW.jpg)  

##### On a default Task list just one line:

```javascript
          var overrides = iCSR.overrides();
          SPClientTemplates.TemplateManager.RegisterTemplateOverrides( overrides );
```

##### will produce:

*all iCSR templates can be cofigured as per above example*

![](http://i.imgur.com/oxedw2u.jpg)

##### *{Haven't had time yet for a 5 minute video}*

## Project goal: make CSR development as easy as possible

For the full story see: [Why I wrote iCSR.js](iCSR-why-it-was-developed.md)

In short:

* Help people get started with CSR development in 5 minutes  
(including installing the [**Cisar Chrome extension**](https://chrome.google.com/webstore/detail/cisar/nifbdojdggkboiifaklkamfpjcmgafpo?hl=en) *developed by Andrei Markeev*)
* Let people learn more JavaScript development by disecting the [iCSR.js](./iCSR.js) source code.
* No dependencies at all on jQuery, Angular, Bootstrap or **any** other .JS and .CSS files

## ![](http://th.downloadblog.it/h57RNZTWa_IIoH3Y9fs71eZKLwI=/64x64/http://media.downloadblog.it/e/e64/steve-jobs-apple.jpg) oh.. and one more thing.. ehm.. line of code..

        iCSR.Interactive = true; // which is the default setting

##### Makes fields fully interactive in Views... who needs Forms?

![](http://i.imgur.com/TKbGDpS.jpg)

## Installation & Usage

1. ##### Install and learn to use the [Cisar Chrome extension](https://chrome.google.com/webstore/detail/cisar/nifbdojdggkboiifaklkamfpjcmgafpo?hl=en) (*developed by Andrei Markeev*)

2. ##### Add [iCSR.js](./iCSR.js) to your Site Collection Style Library  (*or reference the demo library for a quick start*)

3. ##### Use the [iCSR-Templates](iCSR-Templates.md)

4. ##### Or create your own Template:

The new [Office365 Microsoft Planner](http://www.learningsharepoint.com/2016/01/27/10-things-to-know-about-office-365-planner/) breaks Tasks in 4 States:

    0. Not Started (yellow)
    1. Late (red)
    2. In progress (blue)
    3. Completed (green)

##### To add an iCSR Template with the same Planner colorscheme for a standard SharePoint Tasks list:

            "DueDate" : {
                          View: iCSR.Planner
                        }

![](http://i.imgur.com/VFwkN2L.jpg)

## The ONLY code required is:

```javascript
	iCSR.Template('Planner', function () {
                var status = this.Item.Status;
                this.color=2;
                if (status === 'Not Started') {
                    this.color=0;
                } else if (status === 'Completed') {
                    this.color=3;
                } else if (this.days < 0) {
                    this.color=1;
                }
            },
                {
                    rowcolor:true
                }
	);
```

Notes:
* the [Office365 Microsoft Planner](http://www.learningsharepoint.com/2016/01/27/10-things-to-know-about-office-365-planner/) colors are predefined by iCSR.js as: msYellow, msRed, msBlue, msGreen
* iCSR corrects the textcolor for background colors
* iCSR does all pre-configuration and execution for you:
  * so '*this*' refers to one ListItem Due Date
  * contains all the information about that Item ( *this.Item* )
  * and Today calculations you (may) want to use ( *this.days* )
  * *this.output* ,

  *not needed in this code, because it uses the default setting:*

        "<div class='[Class]' style='background:[color];color:[textcolor]'>[value]</div>"

  * is parsed by iCSR to create valid HTML
  * which is then displayed by SharePoint

## Tracing what iCSR does
iCSR source-code is broken up in generic descriptive functions to be used in your custom fields.

Making learning JavaScript hopefully a bit easier.

iCSR has multiple (configurable) levels of console.log traces that can be activated with:

        iCSR.traceon( 3 , true ); // tracelevel:0-5 , clear console


![](http://i.imgur.com/NkVJTL7.jpg)

## License

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">iCSR.js</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://365CSI.nl" property="cc:attributionName" rel="cc:attributionURL">365CSI</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.<br />Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="http://iCSR.github.io" rel="dct:source">http://iCSR.github.io</a>.

#### In normal words:
* CC: You are allowed to use this library for **all** (including commercial) purposes
* BY: You may **not** remove the attribution from the source-code
* That's it

## Version History

* 1.0 - public release february 1st 2016
* 1.1 - not made public
* 1.2 - friday february 5th
    * simplified ``iCSR.Me`` usage (javascript .bind notation is no longer needed)
    * enhanced [token] replace functionality
    * Progressbar now has a reset to 0 on mouseover
* 1.3 / 1.4 - had so much fun with new functionality I never pushed them
* 1.5 - wednesday february 10th
    * major color enhancements
    * added ``rowcolor`` and ``cellcolor`` options
    * with automatic calculation of contrasting text-colors
    * added more inspectors (type **ic** in developer-console)

----------

Amsterdam, february 2016

:email: [Danny Engelman](mailto:danny@engelman.nl)

![](http://i.imgur.com/TKbGDpS.jpg)
