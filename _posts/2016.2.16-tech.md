###内存泄露
* 引用Activity的ClipBoardManager导致内存泄露
	* 解决方案，把Activity改成ApplicationContext
	
===

###性能优化


===

###疑难杂症
* emoji乱码问题
	* 原因：String.subString() [可能]把emoji字符裁剪，导致emoji字符不完整
	* 解决方案：
	* 把字符转成unicode，然后匹配emoji_unicode_hashmap（缺点：循环校验，字符多会很慢）
	*  		/**
    		*判断最后一个字符串最后一个是否是乱码，是则删除
 			*@param text
 			*@param index
 			*@return
 			*/
    		public static boolean isDeleteLastOne(String text, int index) {
    		int unicodelast = text.charAt(index);
    		if (unicodelast == 0xd83d || unicodelast == 0xd83c) {
        		return true;
    		}
    		return false;
	} 
* EditText获取焦点且光标无法去除，把ListView隐藏即会出现这个问题
* GestureDetector的onFling()方法，当按下时，这时如果屏幕有按钮，然后点击按钮，这时onFling()中传递下来的MotionEvent会为空，原因是按钮消费的事件把obtain()中MotionEvent替换并且消费清空了
* GridView的BaseAdapter中的getView()，如果对itemView每次setLayoutParams，在调用itemView的getLocationOnScreen会导致首个itemlocation均为0,0，原因是setLayoutParams会导致attachInfo为空
* GreenDAO的主键必须为封装类型，必须判空为bind，否则每次传入0，主键就为0
    	
    	Long keyId = emotion.getKeyId();
    	if(null != keyId) {
    		sqLiteStatement.bindLong(1, 	emotion.getKeyId());
		}
* ImageView设置Background，如果这个shape无设置solid，有些手机的solid默认是黑色，导致一些透明像素的图片显示黑色，只要把solid设置成`<solid android:color="@color/transperant" />`即可解决问题
	
===

