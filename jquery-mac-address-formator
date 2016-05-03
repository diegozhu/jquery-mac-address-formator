/** 自动对input 和textarea进行mac地址格式化
 $(select).triggerInputMac({ upperCase: true/false , splitor : ":" });
 $(select).destroyInputMac();
 upperCase  为true的时候,转为大写,false转为小写, null 不转换.


automatically format user input string to mac address of input/textarea

*/
(function($) {
	var MacKeydown,MacKeyup,MacKeyblur;
	$.fn.extend({
		triggerInputMac : function(arg){
			if(this.attr("type") != "text" && this.attr("type") != "textarea"){
				throw this[0].innerHTML + " is not input/text or input/textarea";
				return;
			}
			arg = arg || {};
			var upperCase  = arg.upperCase;
			var splitor = arg.splitor || ":";

			function format(string){
				var mac = string || "";
				var m = "";
				for(var i = 0;i<mac.length;i++){
					var c = mac.charCodeAt(i);
					if((c>96&&c<103)||(c>47&&c<58)||(c>64&&c<71)){
						m = m+mac.charAt(i);
					}
				}
				mac = m.length > 12 ? m.substring(0,12) : m;
				var formatedMac = "";
				var count = 0;
				while(count<mac.length && count < 17){
					formatedMac += mac.charAt(count++);
					if(count%2==0 && count < mac.length){
						formatedMac+= splitor;
					}
				}
				// 最后添加 splitor
				if(formatedMac.length < 15 && (formatedMac.length-2)%3 === 0){
					formatedMac+= splitor;
				}
				if(upperCase == null){
					// 不自动转换大小写
					return formatedMac;
				}
				return upperCase ? formatedMac.toUpperCase() : formatedMac.toLowerCase();
			};
			
			MacKeydown = function MacKeydown(e){
				if(e.keyCode == 32){//空格
					return false;
				}
			}
			MacKeyup = function MacKeyup(e){
				if(e.keyCode == 37 || e.keyCode == 39 || e.keyCode == 8 || e.keyCode == 32){
					// ← & → & backspace & blankspace
					return;
				}
				this.value = format(this.value);
			}
			MacKeyBlur = function MacKeyBlur(){
				this.value = format(this.value);
			}
			this.on("keydown",MacKeydown).on("keyup",MacKeyup).on("blur",MacKeyBlur);
			return this;
		},
		destroyInputMac : 	function(){
			if(this.attr("type") != "text" && this.attr("type") != "textarea"){
				throw this[0].innerHTML + " is not input/text or input/textarea";
				return;
			}
			try{this.off("keydown",MacKeydown)}catch(e){}
			try{this.off("keyup",MacKeyup)}catch(e){}
			try{this.off("blur",MacKeyBlur)}catch(e){}
		}
	});
})(jQuery);
