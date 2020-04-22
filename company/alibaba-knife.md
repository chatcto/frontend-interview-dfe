## 面试题讨论
	
	(function() {
		var
			element,
			Knife = function(el) {
				return new Knife.prototype.init(el);
			}

		Knife.fn = Knife.prototype = {
			constructor: Knife,
			proxy: function(type, aim, fn) {
				element.addEventListener(type, function(e) {
					var e = e || window.event;
					if (e.target.className == aim || e.srcElement.className == aim) {
						var target = e.target || e.srcElement;
						fn(target);
					}
				});
				return this;
			}
		}

		init = Knife.fn.init = function(el) {
			element = document.querySelector(el);
			return this;
		}

		init.prototype = Knife.prototype;



		window.Knife = Knife;
	})();
	var listen = function(target) {
		var parent = target.parentElement;
		var element = parent.parentElement;
		element.removeChild(parent)
	}

	Knife("#J_List").proxy("click", "user-delete", listen);
>alibaba前端面试题解.
