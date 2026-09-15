## trendminer_interface.exceptions.AmbiguousResource

Bases: `TrendMinerError`

Two or more equally valid resources exist for given reference

This occurs when uniqueness is implicitly expected by the method, but not explicitly enforced on the appliance side. For example, when two work organizer objects have the same name, attempts to retrieve them by their name will result in this exception. It is up to the user to resolve this ambiguity on the appliance side, or use a more specific request to retrieve the correct resource (e.g., by identifier instead of name).
