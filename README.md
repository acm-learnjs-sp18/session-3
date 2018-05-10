# Session 3: HTML Templating

## Getting Started

To download this repo, click the brigh green button at the top of this page and select "Download ZIP":

![Screen Shot 2018-05-09 at 5.35.39 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 5.35.39 PM.png)

All the code we'll be doing today will be done in the `start` directory, but you can look at the `final` folder for reference.

Slides here: 

## HTML

### Movie Intro

1. Start by heading into the `index.html` file in the `start` directory. There, you'll see a couple of `TODOs` marked for you already. It should look like this:

![Screen Shot 2018-05-09 at 4.46.02 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 4.46.02 PM.png)

2. Right now, we'll be tackling the `MOVIE INTRO` todo.

3. Every Handlebars template starts with a `<script type="text/x-handlebars-template">` tag. Ours will have the additional property of having an `id` called "movieIntro". Add the following script tag:

   ```html
   <script type="text/x-handlebars-template" id="movieIntro"> 
               
   </script>
   ```

4. Inside our script tag, we're going to add a div with the `class` of "movieWrapper." This will be used by our JavaScript later!

   ```html
   <script type="text/x-handlebars-template" id="movieIntro"> 
   	<div class="movieWrapper">
   
   	</div>
   </script>
   ```

   ![Screen Shot 2018-05-09 at 4.48.15 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 4.48.15 PM.png)

5. Time to jump in to our very first Handlebars code! We'll be defining a `<div>` tag that will display all our heroes' names. `<h3>` will be used to show the details on each hero.

   ```html
   <div class="title">{{name}}</div>
   <h3>{{details}}</h3>
   ```

6. Now time to get some actually useful information about our movie! We'll be doing this with a `{{with}}` expression in Handlebars:

   ```handlebars
   {{#with production}}
   	<div> {{year}} - {{director}} - {{production_company}}-{{distrubution_company}} </div>
   {{/with}}
   ```

   By now, your code should look like this:

   ![Screen Shot 2018-05-09 at 4.54.11 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 4.54.11 PM.png)

7. To have some interactivity on our site, let's have an `{{if}}` statement. Put the following code underneath what we have so far. 

   ```handlebars
   {{#if nearby_theater}}
       <h3> Go watch now at {{nearby_theater}} </h3>
   {{else}}
       <h3> Showing nowhere near you :(</h3>
   {{/if}}
   ```

   This will display the nearest theater to you to watch Marvel's "Infinity War." 

   ![Screen Shot 2018-05-09 at 4.59.13 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 4.59.13 PM.png)

8. Time to actually do something with our heroes using an `{{each}}` loop.

   ```handlebars
   {{#each heroes}}
       <div class="heroWrapper">
           {{! Done for each hero }}
           <div>{{name}} {{#format_name}}{{real_name}}{{/format_name}}</div>
       </div>
   {{/each}}
   ```

   Put the above code between our `{{with}}` and `{{if}}` expressions.

9. Now, wrap the `{{each}}` loop in an `<h3>` tag to let us know who's "starring" in the film!

10. The code should look this by now:

    ![Screen Shot 2018-05-09 at 5.05.43 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 5.05.43 PM.png)

### Heroes

11. Now that we got our "movie intro" script down, let's move on to giving our heroes some formatting.

12. Start by finding the `TODO` labelled "TODO: Heroes" and underneath declare the same `<script type="text/x-handlebars-template">` we did earlier, but this time with the `id` of "heroList".

    ```html
    <script type="text/x-handlebars-template" id="heroList"> 
    
    </script>
    ```

13. We're going to add a `div` with the `class` of "title" to give our heroes a nice introduction.

    ```html
    <div class="title">The Heroes</div>
    ```

14. Your code should look like this at this point:

    ![Screen Shot 2018-05-09 at 5.10.20 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 5.10.20 PM.png)

15. Now time to use our friend from earlier: the `{{each}}` loop to iterate through our heroes' data and display them on the page!

16. Declare another `{{each}}` loop and inside it put a `div` with the `class` of "heroList";

    ```handlebars
    {{#each heroes}}
        <div class="heroList" id="{{name}}">
    
        </div>
    {{/each}}
    ```

17. Put the following Handlebars snippet **inside** the "heroList":

    ```handlebars
    <h1>{{name}}</h1>
    <h3>Real Name:</h3>
    <div>{{real_name}}</div>
    <h3>Powers:</h3>
    <div>{{powers}}</div>
    <h3>Abilites:</h3>
    <div>{{abilities}}</div>
    ```

18. Alrighty, at this point, you should have this for your list of heroes:

    ![Screen Shot 2018-05-09 at 5.13.24 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 5.13.24 PM.png)

19. Tying together the previous two sections, in your `index.html` you should have this:

    ![Screen Shot 2018-05-09 at 5.14.12 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 5.14.12 PM.png)

## JavaScript

1. Now let's move to our `main.js` file. Your boilerplate should look like this:

   ![Screen Shot 2018-05-09 at 5.15.28 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 5.15.28 PM.png)

   As you can see, we've only defined two helper functions for you, and the rest are To-Do's.

2. So, let's start with `TODO` number 1 that reads "Get Template Content." Insert the following:

   ```javascript
   var template = document.getElementById("movieIntro").innerHTML;
   ```

3. Now: rendering the template content.

   ```javascript
   var renderer = Handlebars.compile(template);
   var result = renderer(movie);
   ```

   This uses Handlebar's `compile` function to take what we just defined above (the `template` variable) and use it to fill the template with all the actually useful content. But how do we use it?

4. Well, below what we just typed, also put the next line of JavaScript to update the screen:

   ```javascript
   document.getElementById("movieContainer").innerHTML = result;
   ```

5. Okay, so that's all fine and good, but what about characters like "Groot" or "Thanos"? Do we really want to say "Groot as Groot" or "Thanos as Thanos"?

   Probably not! That's why it's time to tackle **helpers** in Handlebars.

   (Before we move on, make sure your code in `main.js` looks like the following picture)

   ![Screen Shot 2018-05-09 at 5.22.03 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 5.22.03 PM.png)

6. Navigate the helper at the very top called `format_name` and define the following variable inside the function:

   ```javascript
   var newHTML = "<i>("+ options.fn(this) + ")</i>";
   ```

7. Now time for the actual logic of our code! This is going to be done in an `if` statement that checks if the character's name is also their "real" non-superhero name:

   ```javascript
   if (this.name.toLowerCase() != this.real_name.toLowerCase()) {
       return newHTML;
   } else {
       return;
   }
   ```

8. Ok, so I know that that was a lot, so let's do a code recap for all the previous steps:

   ![Screen Shot 2018-05-09 at 5.25.46 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 5.25.46 PM.png)

9. Perfect! We have our movies and heroes listed, but we should probably give a little more information about our friendly neighborhood movie stars. For that, let's go to bottom `TODO` that looks identical to the one we just filled out, but without any of the actual code.

10. You're actually going to the exact same thing we did in steps 2-4, but with "heroList" and "heroContainer" instead of "movieIntro" or "movieContainer."

    ```javascript
    //1. Get Template Content
    var template = document.getElementById("heroList").innerHTML;
    
    //2. Render Template
    var renderer = Handlebars.compile(template);
    var result = renderer(movie);
    
    //3. Put rendered HTML back into document
    document.getElementById("heroContainer").innerHTML = result;
    ```

11. Ok, so far we have a pretty good looking page! But wouldn't it be cool if we could link to even *more* information about every hero? After all, they do a lot for us!

12. For that, let's move up to the `link_hero` helper function, defined already right below the `format_name` helper we filled out earlier.

13. Fill it with the following code:

    ```javascript
    var newHTML = "<a href='#" + this.name + "'>"+ options.fn(this) + "</a>";
    return newHTML;
    ```

14. Now, your `main.js` file should look like this:

    ![Screen Shot 2018-05-09 at 5.32.17 PM](/Users/dustinnewman/Desktop/Screen Shot 2018-05-09 at 5.32.17 PM.png)

15. And that's it!

## Wrapping Up

We hope you enjoyed ACM Hack's presentation on HTML Templating with Handlebars.js! Make sure to come next week for our discussion on Node.js + Express.