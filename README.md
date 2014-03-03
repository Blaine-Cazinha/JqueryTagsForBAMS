JqueryTagsForBAMS
=================

AjaxSupport.js: Custom support for Ajax calls to a MVC 4.5 enviroment
    Author: Blaine Cazinha

    This script is split into 5 different functions:
        POST Form:
            Description: This overides the normal html post with an Ajax one and then post the results back to the target element
            Event: submit
            Html Element: <form action="??" method="??">
            Parent Class: main-content (This is from MVC and is located in the _Layout page right before render body function)
            Hooks: data-post-ajax="true" to tie the event, 
                    data-post-target="your identifier here" to identify the target element to be replaced
            Controller signiture input additions: FormCollection collection
            Controller additions: Code to handle an Ajax request and method of "POST"

        Button Filter:
            Description: A button that when press sends a call to the controller to filter by your string
            Event: single_double_click (A third party snippet that does the wait for single or double click)
            Html Element: <input>
            Hooks: data-filter-button-ajax="true" to tie event, 
                    data-filter-type="some filter name" the name you will pass to the controller,
                    data-filter-action="Your URL" the path to your controller (you can use @Url.Action() helper),
                    data-filter-target="your identifier here" to identify the target element to be replaced
            Controller signiture input additions: string filter = ""(for old search item),string search = ""
            Controller additions: Code to handle an Ajax request and a switch/case or nested ifs to filter on
            Dependicies(going to fix this to be more modular): To remember the old search, if it is decending, and filter, your model needs to have three fields
                Html Element:<input type=hidden" id="oldSearch">
                Html Element:<input type=hidden" id="oldFilter">
                Html Element:<input type=hidden" id="oldDecend">
                Hook: data-search-old="old things here from, the model"


        Searching (With autocomplete):
            Event: submit
            Html Element: <form action = "??" method = "??">
            Hooks: data-search-ajax="true" event tie in,
                    data-search-target="your identifier here" to identify the target element to be replaced
            Controller signiture input additions: string filter = "",string search = ""(for old filter item)
            Controller additions: Code to handle an Ajax request and code to search on this (entity framework has StartsWith(term))
            Dependicies(going to fix this to be more modular): To remember the old search, if it is decending, and filter, your model needs to have three fields
                Html Element:<input type=hidden" id="oldSearch">
                Html Element:<input type=hidden" id="oldFilter">
                Html Element:<input type=hidden" id="oldDecend">
                Hook: data-search-old="old things here from, the model"
            To Add Autocomplete
                Html Element:<input>
                Hook: data-search-autocomplete for wire the event to,
                Dependant:
                    Html Element:<form action="??" method="??">
                    Hook: data-search-target="your identifier here" to identify the target element to be replaced

        Pageation:
            Description: Take the functionality of PagedList and makes it Ajaxy (if that was a word)
            Event: click
            Parent Class: main-content (This is from MVC and is located in the _Layout page right before render body function)
            Html Element: @Html.PagedListPager
            Controller signiture input additions:int page=1
            Controller additions: Where ever you call .ToPagedList() put the page in there
            Dependant:
                Html Element:<div class="pagedList">
                Hook: data-pagging-target="your identifier here" to identify the target element to be replaced
            Dependicies(going to fix this to be more modular): To remember the old search, if it is decending, and filter, your model needs to have three fields
                Html Element:<input type=hidden" id="oldSearch">
                Html Element:<input type=hidden" id="oldFilter">
                Html Element:<input type=hidden" id="oldDecend">
                Hook: data-search-old="old things here from, the model"
            Comment: if you just wrap the @Html.PagedListPager in the dependant div this function will work

        Selector: under development
