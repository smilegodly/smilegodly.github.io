---
layout: post
title: "PR to microsoft/vscode"
date: 2019-10-20
---
I decided to try out a pull request in vscode. The feature I added is a button to clear the search bar in the settings editor part of vscode. This feature is helpful if you want to clear the search bar while browsing results as the clear search option that is currently implemented doesn’t pop up on search results. Last I checked all the tests have passed for this feature , and, I am hopeful it gets merged 🙂

![clear button](https://user-images.githubusercontent.com/35276477/67152162-22dad780-f29f-11e9-978f-792fb9144bb3.png)


You can see the button I added in the right side of the search bar.
The main code that I added to vscode, to implement this feature was:

A function I wrote which clears the searchbar...

{% highlight ts %}
clearSearch(): void {
        this.clearSearchResults();
        this.focusSearch();
}
{% endhighlight %}

The code that checks when to enable to clear button.. This code checks if there is input inside the search bar whenever the input changes, and, when it does it will enable the clear button. 

{% highlight ts %}
this._register(this.searchWidget.onInputDidChange(() => {
    const searchVal = this.searchWidget.getValue();
    clearInputAction.enabled = !!searchVal;
    this.onSearchInputChanged();
}));
{% endhighlight %}

A container to place the ActionBar object, The actual ActionBar object to place the button inside, and then the push to the action bar which instantiates the clear button inside the ActionBar.

{% highlight ts %}
this.actionsContainer = DOM.append(searchContainer, DOM.$('.settings-clear-widget'));
 
this.actionBar = this._register(new ActionBar(this.actionsContainer, {
    animated: false,
    actionViewItemProvider: (action: Action) => { return undefined; }
}));
 
this.actionBar.push([clearInputAction], { label: false, icon: true });
{% endhighlight ts %}

Link to issue – [https://github.com/microsoft/vscode/issues/66141](https://github.com/microsoft/vscode/issues/66141)

Link to PR – [https://github.com/microsoft/vscode/pull/82904](https://github.com/microsoft/vscode/pull/82904)
