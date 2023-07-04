# TYPO3 v12.4 - Indexed Search - Searchbox with Bootstrap v5.3.0
Show a Searchbox for Indexed Search on all pages in the Bootstrap Navbar 
## Add targetPid of Indexed Search to Fluid Template
my_site_package/Configuration/TypoScript/setup.typoscript
```
page = PAGE
page {
    typeNum = 0
    shortcutIcon = EXT:my_site_package/Resources/Public/Icons/favicon.ico
    #### Begin Fluidtemplate ####
    10 = FLUIDTEMPLATE
    10 {
    }
    settings {
	    pageIds.search = {$plugin.tx_indexedsearch.settings.targetPid}
    }
}
```
## Searchbox Partial (Bootstrap 5.3.0 sample configuration)
my_site_package/Resources/Private/Partials/Page/Navigation/Search.html
```
<form class="d-flex" role="search" method="post" action="{f:uri.page(pageUid:'{settings.pageIds.search}',additionalParams:'{tx_indexedsearch_pi2: {action:\'search\',controller:\'Search\'}}')}">
  <input class="form-control me-2" type="text" placeholder="Search" aria-label="Search" name="tx_indexedsearch_pi2[search][sword]" value="">
  <button class="btn btn-outline-success" type="submit">{f:translate(key: 'form.submit', extensionName: 'IndexedSearch')}</button>
</form>
```
## Include Searchbox Partial in Bootstrap Navbar (Bootstrap 5.3.0 sample configuration)
my_site_package/Resources/Private/Partials/Page/Navigation/Navbar.html
```
<nav class="navbar navbar-expand-md navbar-dark bg-dark mb-4">
	<a class="navbar-brand" href="#">Navbar</a>
	<button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
	<span class="navbar-toggler-icon"></span>
	<div class="collapse navbar-collapse" id="navbarNav">
		<ul class="nav navbar-nav me-auto mb-2 mb-md-0">
        		<li class="nav-item">
          			<a class="nav-link active" aria-current="page" href="#">Home</a>
        		</li>
        		<li class="nav-item">
          			<a class="nav-link" href="#">Link</a>
        		</li>
		</ul>
		<f:render partial="Navigation/Search" arguments="{_all}"/>
	</div>
</nav>
```
