## trendminer_interface.exceptions.ResourceNotFound

Bases: `TrendMinerError`

Resource does not exist or is not accessible to the current user

Can be raised directly from the code (e.g. a results was expected from a search, but none was found), or through a 404 Not Found response from the API.
