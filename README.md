<div align="center">
<h1>EOS | Dev Guide</h1>
<em>Warning: the code line numbers refer to the latest code pushed in GitHub at the moment of writing (29.10.2019)</em></br></br>
</div>


## A note on notation

- `something written like this` is a piece of code, e.g `print('hello, world')`
- *something written like this* is a piece of architecture, e.g *backend*
- **something written like this** is a important, e.g **mind the gap**


## Change of 'files checkboxes'

**tl;dr**: just change the *frontend* part, the *backend* will adapt itself.

### *frontend*
See how the code mirrors exactly the web-page:

![frontend 2 code](img/frontend2code.png)

To change `FilesCheckboxes`, edit [`FilesCheckboxes`](https://github.com/eos-sns/frontend/blob/master/src/_components/forms/SearchForm.jsx#L187): it is a [ReactJs component](https://reactjs.org/docs/components-and-props.html) which has `'coeval_kZ', 'coeval_PS_z'` labels. Every time the user interacts with it, it calls [`this.handleCheckboxChange`](https://github.com/eos-sns/frontend/blob/master/src/_components/forms/SearchForm.jsx#L39) which updates the ReactJs component state with the new 'files'. Just add a `label` (and its description) to add a parameter). **Change the [initial state](https://github.com/eos-sns/frontend/blob/master/src/_components/forms/SearchForm.jsx#L23) too**.

When a user submits the search, the `searchParams` are encoded in [`postSearch`](https://github.com/eos-sns/frontend/blob/master/src/_services/search.service.js#L10); then the data is transferred to *backend*.

### *backend*
[`searchByParams`](https://github.com/eos-sns/backend/blob/master/search/search.service.js#L12) will forward the request to *mercurius*, the local Flask server that handles the queries. The search request is a *POST* request: it is handled by [`handle_post_request`](https://github.com/eos-sns/mercurius/blob/master/mercurius/server.py#L16) which parses [user, parameters and files](https://github.com/eos-sns/mercurius/blob/master/mercurius/req/handlers.py#L118).

### *mercurius*
*mercurius* then creates an istance of `Helios` inside [`handle_query`](https://github.com/eos-sns/mercurius/blob/master/mercurius/req/handlers.py#L83) to handle the query. `helios` then saves to disk the data (with the required files](https://github.com/eos-sns/helios/blob/master/helios/helios/h5.py#L53).


## Authors
| [![sirfoga](https://avatars0.githubusercontent.com/u/14162628?s=128&v=4)](https://github.com/sirfoga "Follow @sirfoga on Github") |
|---|
| [Stefano Fogarollo](https://sirfoga.github.io) |


## License
[Unlicense](https://unlicense.org/)
