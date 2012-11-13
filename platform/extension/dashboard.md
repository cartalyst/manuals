###Dashboard

----------

#### Introduction

The Dashboard is a generic admin page that acts as the home page after initial login. It is a great place to present information based data to your admin users.

-----------

#### Screencast

-----------

#### Basic Usage

The dashboard page is essentially just a template for you to display any widgets or custom data you may want to show an administrator when they login or first visit the admin page. To modify whats seen, simply find the dashboard extension in your backend themes directory, and add widgets, custom html or whatever it is you may want to your dashboards content.


Example of displaying last 5 registered users in an existing dashboard. Note that this is an example, the widget call may or may not exist.

	@layout('templates.default')

	<!-- Page Title -->
	@section('title')
		{{ Lang::line('platform/dashboard::dashboard.title') }}
	@endsection

	<!-- Queue Styles | e.g Theme::queue_asset('name', 'path_to_css', 'dependency')-->

	<!-- Styles -->
	@section ('styles')
	@endsection

	<!-- Queue Scripts | e.g. Theme::queue_asset('name', 'path_to_js', 'dependency')-->

	<!-- Scripts -->
	@section('scripts')
	@endsection

	<!-- Page Content -->
	@section ('content')
		<!-- get last 5 registered users -->
		<div id="users">
			@widget('platform/users::registered.last', 5)
		</div>
	@endsection


-----------