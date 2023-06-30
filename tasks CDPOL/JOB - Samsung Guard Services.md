27.06.2023
[[CDPOL-5452] Samsung Guard Serwis / Update - Jira (atlassian.net)](https://cheil.atlassian.net/browse/CDPOL-5452)

<hr>

git copy from gitlab
[techcenter / AEM pages / 3 lata guard serwis · GitLab (cheil.io)](https://gitlab.cheil.io/techcenter/aem-pages/3-lata-guard-serwis)
make changes
build "gulp build"
edit/create AEM and start qa for qa
create branch and pull req for gitlab ???

<hr>
## node.js / npm downgrade to run 

"gulp": "^3.9.1",

 If you are short on time, downgrade Node.js to v11.* or below; if you need newer features, and have time to possibly fix a load of broken dependencies, upgrade Gulp to 4.* or above!

nvm use 10.16.3
npm install -g npm@6.14.15

in nvm on windows npm install manualy

<hr>

1. overlaping title-header: 
   The issue with the overlapping `<span>` element is likely due to the presence of the `<br>` element inside the `<span>`. By default, `<span>` elements are inline elements, meaning they do not create line breaks. However, when you include a `<br>` element within a `<span>`, it can cause unexpected layout behavior.
   1.Remove the `<br>` elemen
   2.Use CSS to manage the layout:
   ```js
	<span class="title-header">Samsung Guard Serwis<br class="visible-md" /></span>
```
3. edit br
```xml
// add space between lines
.title-header {
  br.visible-md {
    @media (min-width: 720px) {
      content: ""; /* clears default height */
      margin-top: 15px; /* change height  */
    }
    @media (min-width: 1024px) {
      margin-top: 25px;
    }
  }
}
```


<hr>

2. change hero img 
	dont have access to p5 :
	//images.samsung.com/is/image/samsung/p5/pl/3latgw/img/desktop_kv.png?$ORIGIN_PNG$?$ORIGIN_PNG$
	
	how to get to images.samsung.com ?

	same as in UK json stuff, it's that graphql thing with url, and don't need access :
	1. put to AEM img
	2. //images.samsung.com/is/image/samsung/assets/ + pl/campaign/3-lata-guard-serwis/pc_hero.png?$ORIGIN_PNG$
	3. pl/campaign/3-lata-guard-serwis/pc_hero.png?$ORIGIN_PNG$ => this is last url from where you put img in AEM 
	4. when got pdf, first part of url like this = //images.samsung.com/is/content/samsung/assets/
		1. change /image/ for /content/
		5.
	
	
	<hr>

4. update regulations ?
 where paste and how to href that pdf ?
 
  when got pdf, first part of url like this = //images.samsung.com/is/content/samsung/assets/
		1. change /image/ for /content/
 
<hr>

5. img tumbnails
 need new one - with no background
 got it
 
 <hr>

6. add title to steps with <h5/> and align to left in some 
```@media (min-width: 425px) and (max-width: 719px) {
      h5 {
        text-align: left;
      }
  }
```
<hr>