(function($, undefined) {

	"use strict";

	$(function() {
		
		var $form = $( "#yourIDForm" ); //change your ID form.
		var $input = $form.find( "input" ); //change your input class, id convert. Ex: input.yourClassInput. With class yourClassInput in input convert.

		$input.on( "keyup", function( event ) {
			
			var selection = window.getSelection().toString();
			if ( selection !== '' ) {
				return;
			}
			if ( $.inArray( event.keyCode, [38,40,37,39] ) !== -1 ) {
				return;
			}
			
			
			var $this = $( this );
			var input = $this.val();
			
			var input = input.replace(/[\D\s\._\-]+/g, "");
					input = input ? parseInt( input, 10 ) : 0;

					$this.val( function() {
						return ( input === 0 ) ? "" : input.toLocaleString( "en-US" );
					} );
		} );
		
		$form.on( "submit", function( event ) {
			
			var $this = $( this );
			var arr = $this.serializeArray();
		
			for (var i = 0; i < arr.length; i++) {
					arr[i].value = arr[i].value.replace(/[($)\s\._\-]+/g, ''); 
			};
			
			console.log( arr );
			
			event.preventDefault();
		});
		
	});
})(jQuery);