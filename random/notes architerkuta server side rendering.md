devstyle.pl


1. Rodzaje architektur

MPA - Multi Page App do 2004

AJAX od 2004 

SPA - Single Page App  
	np. React

SSR - Server-Side Rendering
	np. React-Next.js

SSG - Static Site Generation

Incremental Static Generation
	np. Gatsby.js : 
		- oferuje SSG, SSR
		- dużo dziwacznych rozwiązań i pluginów

Island Architecture ?

Co robi qwik ? => rozbija aplikacje na mniejsze części ktore pobiera te malutkie części kiedy potrzeba => Qwik Progressive Hydration => better hydration

React Server Components
use server
	client side components - hydrated - interactive
use client
	server side components - not hydrated - not interactive

"Hydracja" => DOM - VDOM - reconcile - client react take over
	hydrateRoot ()