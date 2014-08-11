Dynamic-Type
============

Dynamic Type JQuery plugin based off Material Design

```;
(function ($) {
	$.fn.dynamicType = function (options) {
		var fontSizes =   (options.fontSizes) ? options.fontSizes : [90,  72, 60, 48, 36, 30, 24, 18, 14, 13, 12];
		var lineHeights = (options.lineHeights) ? options.lineHeights : [108, 90, 72, 60, 48, 36, 30, 24, 20, 20, 18];
		$(this).each(function() {
			var maxHeight = $(this).height();
			var maxWidth = $(this).width();
			var text = $('<p>' + $(this).html() + '</p>');
			$(this).html(text);
			var textHeight = text.height();
			var textWidth = text[0].scrollWidth; // true width
			var index = 0;
			do {
				text.css('font-size', fontSizes[index]).css('line-height', lineHeights[index] + 'px');
				textHeight = text.height();
				textWidth = text[0].scrollWidth;
				index++;
				if (index >= fontSizes.length) {
					$(this).dotdotdot();
					text = $(this).find('p')
					textHeight = text.height();
				}
			} while ((textHeight > maxHeight || textWidth > maxWidth) && index < fontSizes.length);
			// Now vertically centre
			text.css('margin-top', (maxHeight - textHeight)/2 + 'px');
		});
	}
})(jQuery);