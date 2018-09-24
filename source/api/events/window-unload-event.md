---
title: window:unload
---

The `window:unload` event fires when your application is has unloaded and is navigating away. The real event object is provided to you. This event is not cancelable.

# Environment

Some events run in the {% url "browser" catalog-of-events#Browser-Events %}, some in the {% url "background process" background-process %}, and some in both. {% url "See all events" catalog-of-events#Environment %}.

Event | Browser | Background Process
--- | --- | ---
`window:unload` | {% fa fa-check-circle green %} | {% fa fa-times-circle grey %}

# Arguments

**{% fa fa-angle-right %} event** ***(Object)***

The `beforeunload` event.

# Usage

## In the browser

In a spec file or support file you can tap into the `window:unload` event.

```javascript
cy.on('window:unload', (e) => {

})
```

# Examples

## Test that your application was redirected

```javascript
// app code
$('button').on('click', (e) => {
  // change the page programmatically
  window.location.href = '/some/new/link'
})

// test code
it('redirects to another page on click', function (done) {
  // this event will automatically be unbound when this
  // test ends because it's attached to 'cy'
  cy.on('before:window:unload', (e) => {
    // no return value on the event
    expect(e.returnValue).to.be.undefined
  })

  cy.on('window:unload', (e) => {
    // using mocha's async done callback to finish
    // this test so we are guaranteed the application
    // was unloaded while navigating to the new page
    done()
  })

  // click the button causing the page redirect
  cy.get('button').click()
})
```

# See also

- {% url `before:window:load` before-window-load-event %}
- {% url `before:window:unload` before-window-unload-event %}
- {% url `window:load` window-load-event %}