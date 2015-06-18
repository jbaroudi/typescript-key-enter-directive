# typescript-key-enter-directive
A Simple port of a key enter directive from @Epokk to Typescript (https://gist.github.com/EpokK/5884263)

	module util {
		'use strict';

		export class KeyEnterDirective implements angular.IDirective {

			public link;

			restrict = 'A';
			scope = false;

			constructor() {
				this.link = this.unboundLink.bind(this);
			}

			unboundLink(scope: angular.IScope, element: JQuery, attributes: any) {
				element.bind('keydown keypress', function(event: JQueryEventObject) {
					if (event.which === 13) {
						scope.$apply(function () {
							scope.$eval(attributes.keyEnter);
						});

						event.preventDefault();
					}
				});
			}

			static instance(): ng.IDirectiveFactory {

				var directive = () => new KeyEnterDirective();
				directive.$inject = [];
				return directive;
			}

		}
	}
	
and it's loaded like this:

	angular.module('myModule', ['ngAnimate', ...])
		.directive('keyEnter', util.KeyEnterDirective.instance())

You can change the directive name ('keyEnter') to decorate your attribute:

	<input key-enter="myFunction()" />

 :D