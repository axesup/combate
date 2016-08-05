### High-level Steps
1. Name your page
2. Create .jade page (HTML)
3. Create .sass page (CSS)
4. Create .coffee page (code)
5. Add URL under codecombat.com
6. Add teacher dashboard menu item

Quick notes:

1. Don't worry about localization (i18n stuff)
2. Indentation is important, always.
3. Changes should be made the main codecombat branch, in a new feature branch
4. Assumes you have a [working dev environment](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-General-Information)

### 1. Name your page (harder than it sounds)

Choose the name of your page wisely, and follow all our naming conventions.

Names chosen for this example:

    ExampleTeacherView
    example-teacher-view
    /example-view

### 2. Create .jade page (HTML)

Put your new HTML file here: `app/templates/teachers/foo-bar-view.jade`

File contents:

    extends /templates/base-flat

    block page_nav
      include ../courses/teacher-dashboard-nav.jade

    block content

      .container
        h1.example_style Hi Mom!

### 3. Create .sass page (CSS)

Put your new CSS file here: `app/styles/teachers/foo-bar-view.sass`

File contents:

    #example-teacher-view
      .example_style
        background-color: fuchsia
        border: 10px dashed olive
        color: darkblue
        height: 500px
        font-size: 40px
        text-align: center

### 4. Create .coffee page (code)

Put your new code file here: `app/views/teachers/FooBarView.coffee`

File contents:

    RootView = require 'views/core/RootView'

    module.exports = class ExampleTeacherView extends RootView
      id: 'example-teacher-view'
      template: require 'templates/teachers/example-teacher-view'

Replace the example names within the file with your own.

### 5. Add URL under codecombat.com

Open this file: `app/core/Router.coffee`

Add this entry to roughly line 153, alphabetized in the /teachers section.

    'teachers/foo-bar': go('teachers/FooBarView')

### 6. Add teacher dashboard menu item (OPTIONAL)

Open this file: `app/templates/courses/teacher-dashboard-nav.jade`

Add this entry to roughly line 153, alphabetized in the /teachers section.

    li(class= path.indexOf('/teachers/foo-bar') === 0 ? 'active' : '')
      a(href='/teachers/foo-bar')
        small.label Foo Bar

### Done!

You should now be able to navigate to `http://localhost:3000/teachers/foo-bar`

**Changed files in your local GitHub repository**

    14:29:00:~/GitHub/codecombat$ git status
    On branch master
    Your branch is up-to-date with 'origin/master'.
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
    
    	modified:   app/core/Router.coffee
    	new file:   app/styles/teachers/example-teacher-view.sass
    	modified:   app/templates/courses/teacher-dashboard-nav.jade
    	new file:   app/templates/teachers/example-teacher-view.jade
    	new file:   app/views/teachers/ExampleTeacherView.coffee

Now go submit a pull request for your awesomely static teacher page!