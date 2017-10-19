# vue.js
智能社：Javascript之vue.JS(一） {录播} 
1. 认识Vue  
2. vue和angular的区别？  
3. vue基本雏形  
4. 认识vue里面几个常用的指令
  window.onload=function(){
            var c=new Vue({
                el:'#box',
                data:{
                    msg:'welcome vue',
                    json:{a:'1'},
                    arr:['apple','orign','pear'],
                    show:true
                },
                methods:{
                	add:function(){
                		//this.arr.push('balana');
                		this.show = false;
                	}
                }
            });
  };
  数组:
  <ul>
      <li v-for="(item,index) in arr">
        {{item}}  {{index}}
      </li>
  </ul>
  JSON:
  <ul>
    <li v-for="(val,key) in json">{{key}}{{val}}</li>
  </ul>
5. bootstrap+vue的简易留言  
  bootstrap就是设置class
6. 其他指令全面认识？  
7. computed的使用  
8. 属性和事件
  事件:
  1.v-on:click=""
  2.@click
  
  1.v-on:click="show($event)"   ev.keycode = '12'
  2.@click.enter="show"
  事件冒泡:
  1.@click="show($event)"   ev.cancleBubble();
  2.@click.stop = "show()"
  默认行为:
  1.@click="show($event)"   ev.preventDefault();
  2.@click.prevent="show()"
9. class和style  
  数据绑定:
    1.src="{{imgUrl}}"
    2.v-bind:src="imgUrl"
    3.:src="imgUrl"
  设置class、style比较特殊
  1.class
  <style>
	.red{
		background-color:red;
	}
  .blue{
    color:blue;
  }
</style>
<script>
        window.onload=function(){
            var c=new Vue({
                el:'#box',
                data:{
                    msg:'welcome vue',
                    json:{a:'1'},
                    arr:['apple','orign','pear'],
                    show:true,
                    r:"red",
                    b:"blue",
                    c:true,
                    d:false,
                    jsonClass:{red:c,blue:d},
                    width:{width:"50px"},//json格式,与class的数组形式的不同
                    height:{height:"50px"}
                },
                methods:{
                	add:function(){
                		//this.arr.push('balana');
                		this.show = false;
                	}
                }
            });
        };
</script>
1.使用数组的形式引用vue中的数据：
<div style="width:100px; height:100px" :class="[r,b]" v-show="show"/>
2.使用json的形式:
<div style="width:100px; height:100px" :class="{red:true,blue:false}" v-show="show"/>
3.json
<div style="width:100px; height:100px" :class="{red:c,blue:d}" v-show="show"/>
4.json
<div style="width:100px; height:100px" :class="jsonClass" v-show="show"/>

2.style:
  <div :style="[width,height]" />
10. 模板  
  {{msg}} 
  {{*msg}}//数据更新不跟随变化*
  {{{msg}}}//解释成h5
11. 过滤器  
  {{msg | uppercase | lowercase}}
12. vue的交互  
  <script src="https://cdn.jsdelivr.net/vue.resource/1.0.3/vue-resource.min.js"></script>
  
  get:
  <script>
        window.onload=function(){
            var c=new Vue({
                el:'#box',
                data:{
                },
                methods:{
                  /
                	get:function(){
                		this.$http.get('a.txt',{
                			//a:1,   上传的时候需要传输json数据
                			//b:2
                		}).then(function(res){
                			alert(res.status+"-"+res.data);
                		},function(res){
                			alert(res.status);
                		});
                	}
                }
            });
        };
</script>

  post:
  <script>
          window.onload=function(){
              var c=new Vue({
                  el:'#box',
                  data:{
                  },
                  methods:{
                    post:function(){
                      this.$http.post('a.php',{
                        word:'a'
                      },{
                        emulateJSON:true   //post需要加这个
                      }).then(function(res){
                        alert(res.status+"-"+res.data.query);
                      },function(res){
                        alert(res.status);
                      });
                    }
                  }
              });
          };
  </script>
  
  jsonp:
  <script>
          window.onload=function(){
              var c=new Vue({
                  el:'#box',
                  data:{
                  },
                  methods:{
                    post:function(){
                      this.$http.jsonp('https://sug.so.360.cn/suggest',{params:{
                    	  word:'a'
                      }}).then(function(res){
                        alert(res.status+"-"+res.data.s);
                      },function(res){
                        alert(res.status);
                      });
                    }
                  }
              });
          };
  </script>
  
  jsonp：修改callback名字
  <script>
          window.onload=function(){
              var c=new Vue({
                  el:'#box',
                  data:{
                  },
                  methods:{
                    post:function(){
                      this.$http.jsonp('https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su',{params:{
                    	  wd:'a'
                      }},{
                    	  jsonp:'cb'    //callback名字，默认名字就是callback
                      }).then(function(res){
                        alert(res.status+"-"+res.data.s);
                      },function(res){
                        alert(res.status);
                      });
                    }
                  }
              });
          };
  </script>
13. 使用vue制作百度和360搜索下拉框 
智能社：Javascript之vue.JS(二） 
1. 计算属性的使用 
  //a改变b也跟着改变
   <script>
		var c = new Vue({
			el : '#box',
			data : {
				msg : 1
			},
			computed:{//计算参数,其实b也是一个data，只是有逻辑能改变
				b:{
            get : function(){
              return this.msg+2;
            },
            set : function(val){
              this.msg = val;
            }
      }
			}
		});
	
	document.onclick= function(){
		c.msg = 102;
    c.b = 101;//调用set方法
	}
</script>

自定义属性：
<script>
		var c = new Vue({
			aa : 1,
			el : '#box',
			data : {
				msg : 1
			},
			computed : {//计算参数,其实b也是一个data，只是有逻辑能改变
				b : function() {
					return this.msg + 1;
				}
			}
		});

		document.onclick = function() {
			console.log(c.$options.aa);//c.$options是获取自定义属性、
			console.log(c.$data.msg);
      //c.$el    ->设置数据绑定的元素
      //c.$mount  ->手动挂载、相当于设置el
      //c.destory  ->销毁对象
      //c.$log    ->获取data中的数据对象
		}
	</script>
2. 提高循环的性能，让重复数据显示出来 
3. vue实例的简单方法 
4. 自定义过滤器 
5. 自定义指令 
6. 自定义键盘事件 
7. 数据的监听 
8. vue组件 
  组件就是一个大对象.组件其实跟new Vue({})是差不多的.
  全局组件:<aaa></aaa>
  var Aaa = Vue.extend({
			template : '<h3 @Click="show()">{{msg}}</h3>',
			data(){//在组件中data要以函数的形式，并且retuen必须是Json格式的
				return {
					msg : "Hello!"
				};
			},
			methods:{
				show : function(){
					this.msg = "show";
				}
			}
		});
		
	Vue.component('aaa',Aaa);//在整个html中使用aaa
  
  全局的第二种写法:
  Vue.component('my-aaa',{
			template : '<h2>h2</h2>'
	});
  局部组件:
  <script>
		var Aaa = Vue.extend({
			template : '<h3 @Click="show()">{{msg}}</h3>',
			data(){//在组件中data要以函数的形式，并且retuen必须是Json格式的
				return {
					msg : "Hello!"
				};
			},
			methods:{
				show : function(){
					this.msg = "show";
				}
			}
		});
		
		
		var vm = new Vue({
			el:'#box',
			components:{//把component绑定到box标签下，在box下使用aaa，形成局部
				//my-aaa需要加上''
				'my-aaa' : Aaa    
			}
		});
		//Vue.component('aaa',Aaa);
	</script>
  局部第二种：
  var vm = new Vue({
			el:'#box',
			components:{//把component绑定到box标签下，在box下使用aaa，形成局部
				//my-aaa需要加上''
				'my-aaa' : {
          data(){
            return {
              msg : 'msg'
            };
          },
					template : "<h1>h1-{{msg}}</h1>"
				}    
			}
		});
    
    把模板单独放置到template中
    <div id="box">
	
		<my-aaa></my-aaa>
		
		
		<template id="aaa">
			<h1>标题</h1>
			<ul>
				<li v-for="item in fruit">
					{{item}}
				</li>
			</ul>
		</template>
		
		
		<script>
		var vm = new Vue({
			el:'#box',
			components:{//把component绑定到box标签下，在box下使用aaa，形成局部
				//my-aaa需要加上''
				'my-aaa' : {
					template : "#aaa",
					data(){
						return {
							msg:"Welcome",
							fruit:['apple','orign','pear','banana']
						};
					},
					methods:{
						change(){
							this.msg = 'changed';
						}
					}
				}    
			}
		});
		
	</script>
	</div>
  
  <!-- 动态组件 -->
	<div id="box">
		<input type="submit" @Click="a='my-aaa'" value="my-aaa"/>
		<input type="submit" @Click="a='my-bbb'" value="my-bbb"/><br>
		<component :is="a"></component><!-- 标签时Component -->
		
		
		<script>
		var vm = new Vue({
			el:'#box',
			components:{//把component绑定到box标签下，在box下使用aaa，形成局部
				//my-aaa需要加上''
				'my-aaa' : {
					template : "my-aaa"
				},
				'my-bbb' : {
					template : 'my-bbb',
				}
			},
			data : {
				a : "my-aaa"
			}
		});
		
		</script>
	</div>
  
  github vue-devtools
  
  <!--子组件获取父组件的数据，使用template，然后再子组件中使用:m来引用到子组件中，使用props来获取-->
  <div id="box">
		<my-aaa></my-aaa>
		
		<template id="my-aaa">
			<h1>111111  --->{{msg}}</h1>
			<my-aaa-child :m=msg :my-msg=myMsg></my-aaa-child>
		</template>
		
		<script>
		var vm = new Vue({
			el:'#box',
			components:{//把component绑定到box标签下，在box下使用aaa，形成局部
				//my-aaa需要加上''
				'my-aaa' : {
					template : "#my-aaa",
					components:{
						'my-aaa-child':{
							props:{//这样就能拿到了
								m:'',
								myMsg:''
							},
							template : 'my-aaa-child-->{{m}}-->{{myMsg}}',
						}
					},
					data(){
						return {
							msg:'aaa',
							myMsg:'my-msg'//在html中使用-，在js中使用驼峰式
						};
					}
				},
				'my-bbb' : {
					template : 'my-bbb',
				}
			},
			data : {
				a : "my-aaa"
			}
		});
		
		</script>
	</div>
  
  <!--父组件获取子组件的data，在子组件中使用函数返回特定的值、this.$emit、在子组件中使用@child-msg-event监听返回值调用父组件的方法即可-->
  <div id="box">
		<my-aaa></my-aaa>
		
		<template id="my-aaa">
			<h1>我是父级->{{msg}}</h1>
			<my-aaa-child @child-msg-event="get"></my-aaa-child>
		</template>
		
		<template id="my-aaa-child">
			<input @Click="send()" type="submit" value="发送"/>
		</template>
		
		<script>
		var vm = new Vue({
			el:'#box',
			components:{//把component绑定到box标签下，在box下使用aaa，形成局部
				//my-aaa需要加上''
				'my-aaa' : {
					template : "#my-aaa",
					methods:{
						get(childData){
							this.msg = childData;
						}
					},
					components:{
						'my-aaa-child':{
							props:{//这样就能拿到了
								m:'',
								myMsg:''
							},
							template : '#my-aaa-child',
							data(){
								return {
									a : "我是子级"
								}
							},
							methods:{
								send(){
									this.$emit('child-msg-event',this.a);
								}
							}
						}
					},
					data(){
						return {
							msg:'aaa',
							myMsg:'my-msg'//在html中使用-，在js中使用驼峰式
						};
					}
				},
				'my-bbb' : {
					template : 'my-bbb',
				}
			},
			data : {
				a : "my-aaa"
			}
		});
		
		</script>
	</div>
智能社：Javascript之vue.JS(三） 
1. 组件间数据传递、同步数据更新 
2. vue-router 
3. slot的使用 
4. vue-cli、vue-loader 
  <div id="box">
		<ul>
			<li><a v-link="{path:'/home'}">主页</a></li>
			<li><a v-link="{path:'/News'}">新闻</a></li>
		</ul>
		<div>
			<router-view></router-view>
		</div>
		
		<template id="home">
			<h3>我是主页</h3>
			<div>
				<a v-link="{path : '/home/login'}">登陆</a>
				<a v-link="{path : '/home/reg'}">注册</a>
			</div>
			<div>
				<router-view></router-view>
			</div>
		</template>
		
		<template id="News">
			<h3>我是主页</h3>
			<div>
				<a v-link="{path : '/News/detail/001'}">新闻001</a>
				<a v-link="{path : '/News/detail/002'}">新闻002</a>
			</div>
			<div>
				<router-view></router-view>
			</div>
		</template>
		
		<template id="detail">
			{{$route.params | json}}
			{{$route.path}}
			{{$route.query | json}}
		</template>
		
		<script>
			//1、准备根组件
			var App = Vue.extend();
			//2、准备Home、News组件
			var Home = Vue.extend({
				template : '#home'
			});
			var News = Vue.extend({
				template : '#News'
			});
		
			var Detail = Vue.extend({
				template : "#detail"
			});
		
			//3、准备路由
			var router = new VueRouter();
			
			//4、关联
			
			router.map({
				'home' : {
					template : Home,
					subRouters:{
						'login' : {
							component : {
								template : "<strong>我是登陆信息</strong>"
							}
						},
						'reg' : {
							component : {
								template : "<strong>我是注册信息</strong>"
							}
						}
					}
				},
				'News' : {
					template : News,
					subRouters:{
						'/detail/:id' : {
							component : Detail
						}
					}
				}
			});
			
			//5、启动路由器
			router.start(App,"#box");
			
			//6、页面跳转
			router.redirect({
				'/':'/home'
			})
		</script>
	</div>
5. vue-devtools 
6. vue构建SPA应用 
智能社：Javascript之vue.JS(四） 
1.vue-loader和vue-router的结合使用 
2.vue-cli的使用流程 
3.常见报错信息 
4.默认端口的更改 
5. simple、webpack、webpack-simple、 browserify、browserify-simple的项目模板使用 以及推荐 
智能社：Javascript之vue.JS(五） {录播}  
1.vue2.0与1.0的区别 
  1、对于组件的创建：
    Vue.component('my-aaa',{
				template : '#aaa',
        data(){
          return {}
        },
        methods:{
        }
			});
  2、在template中必须有一个根元素进行包裹
    <template id="aaa">
		<div>
			<h4>我是组件</h4>
			<strong>我是加粗标签</strong>
		</div>
	</template>
2.组件模板片段代码的替换 
3.组件的简洁语法定义 
4.生命周期的变化 
  var vm = new Vue({
				el : '#box',
				data : {
					nShow:'SHOW'
				},
				methods : {
				},
				beforeCreate(){
					console.log('beforeCreate');
				},
				created(){
					console.log('created');
				},
				beforeMount(){
					console.log('brforeMount');
				},
				mounted(){
					console.log('mounted');
				},
				beforeUpdate(){
					console.log('beforeUpdate');
				},
				updated(){
					console.log('updated');					
				},
				beforeDestory(){
					console.log('beforeDestory');	
				},
				destoryed(){
					console.log('destoryed');
				}
			});
5.新增生命周期 
6.vue2.0里面的循环变化 
  <div id="box">
		<ul>
			<li v-for="(val,index) in nShow">
				{{val}}-{{index}}
			</li>
		</ul>
	</div>
7.track-by的代替者 
8.自定义键盘指令的替换 
  Vue.config.keyCodes.ctrl = 17;
  <input type="text" @keydown.ctrl="changed()">
9.封杀过滤器 
  <body>
	<script>
		$(function(){
			//自定义过滤器
			Vue.filter('add',function(n,a,b){
				console.log(a+'-'+b);
				return n < 10 ? '	0'+n: ''+n;
			});
			var vm = new Vue({
				el : '#box',
				data : {
					msg : "9"
				}
			});
		});
	</script>
	<div id="box">
		{{msg | add(12,5)}}
	</div>
</body>
10. 2.0里组件通信的问题
  //子组件获取父组件中的数据
  <body>
	<script>
		$(function(){
			var vm = new Vue({
				el : '#box',
				data : {
					a : "我是父组件的数据"
				},
				components:{
					'my-component':{
						props:['msg'],
						template : "#child"
					}
				}
			});
		});
	</script>
	<template id="child">
		<div>
			<h3>我是子组件</h3>
			<strong>{{msg}}</strong>
		</div>
	</template>
	<div id="box">
		<my-component :msg="a"></my-component>
	</div>
</body>
  
//子组件修改父组件的数据，联动
<body>
	<script>
		$(function(){
			var vm = new Vue({
				el : '#box',
				data : {
					myData:{
						a : "我是父组件的数据"
					}
				},
				components:{
					'my-component':{
						props:['msg'],
						template : "#child",
						methods:{
							changed(){
								//修改数据
								this.msg.a = "子组件修改了父组件的数据"
							}
						}
					}
				}
			});
		});
	</script>
	<template id="child">
		<div>
			<h3>我是子组件</h3>
			<strong>{{msg.a}}</strong>
			<button @click="changed()">修改父组件的数据</button>
		</div>
	</template>
	<div id="box">
		会联动修改父组件的数据
		{{myData.a}}
		<!-- 子组件修改父组件的数据的时候，传递父组件的一个json对象，这样的话只是修改对象中属性的值 -->
		<my-component :msg="myData"></my-component>
	</div>
</body>
11. 更加靠谱的组件通信方案: 单一事件管理通信 
	//组件间的通信：Event.$emit()/Event.$on()
	<body>
	<script>
		var Event = new Vue();
	
		var A = {
				template : '#a-template',
				data(){
					return {
						a : '我是A组件数据'
					};
				},
				methods:{
					send(){
						Event.$emit('a-msg',this.a);
					}
				}
		};
		
		var B = {
				template : "<h1>我是组件B</h1>",
				data(){
					return {
						a : '我是B组件数据'
					};
				}
		};
		
		var C = {
				template : `<div><h1>我是组件C</h1>-{{a}}</div>`,//要使用<div>包括起来，不然显示不出来
				mounted(){
					console.log('mounted');
					var _this = this;
					Event.$on('a-msg',function(data){
						console.log(data);
						this.a = data;
					}.bind(this));
				},
				data(){
					return {
						a : 'a'
					}
				}
		};
		
		$(function(){
			var vm = new Vue({
				el : '#box',
				data : {
					
				},
				components:{
					'a-component' : A,
					'b-component' : B,
					'c-component' : C
				}
			});
		});
	</script>
	
	<template id="a-template">
		
		<input type="submit" @click="send()">传输数据到B组件</button>
	</template>
	<div id="box">
		<a-component></a-component>
		<b-component></b-component>
		<c-component></c-component>
	</div>
	</body>
	
智能社：Javascript之vue.JS(六） 
1.vue2.0的过渡(transition) 
   <body>
	<!--使用transation主要定义.fade-leave-active、.fade-leave-enter，使用transition标签包住即可-->
	<div id="box">
		<input type="submit" value="点击" @click="show=!show"/>
		<transition name="fade" 
			@before-enter="beforeEnter"
			@enter="enter"
			@after-enter="afterEnter"
			@before-leave="beforeLeave"
			@leave="leave"
			@after-leave="afterLeave">
			<p v-show="show"></p>
		</transition>
	</div>
	<script>
		$(function(){
			var vm = new Vue({
				el : '#box',
				data : {
					show : true
				},
				methods:{
					beforeEnter(el){
						//el是要使用动画的元素
					},
					enter(el){
						
					},
					afterEnter(el){
						el.style.background='blue';
					},
					beforeLeave(el){
						//el是要使用动画的元素
					},
					leave(el){
						
					},
					afterLeave(el){
						el.style.background='red';
					}
				}
			});
		});
	</script>
</body>


<!--transation与animated进行动画操作、使用transation进行包裹、使用enter-active-class、并在使用动画的标签上使用class="animated"、同时要引入
link-->
<link rel="stylesheet" href="./css/animate.css">
<body>
	<div id="box">
		<input type="submit" value="点击" @click="show=!show"/>
		<transition enter-active-class="bounceInLeft" leave-active-class="bounceOutRight">
			<p v-show="show" class="animated"></p>
		</transition>
		
		<transition enter-active-class="zoomInLeft" leave-active-class="zoomOutRight">
			<p v-show="show" class="animated"></p>
		</transition>
	</div>
	<script>
		$(function(){
			var vm = new Vue({
				el : '#box',
				data : {
					show : false
				},
				methods:{
				}
			});
		});
	</script>
</body>
2.过渡的钩子函数(hook) 
3.多个元素过渡 
4.vue-router2.0的使用 
5.路由和动画结合 
6.vue router2.0的使用  
   1、html：
   	<div id="box">
		<!--定义两个连接-->
		<div>
			<router-link to="/home">主页</router-link>
			<router-link to="/news">新闻页</router-link>
		</div>
		<div>
			<!-- 显示路由 -->
			<router-view></router-view>
		</div>
	</div>
    2、js
    <script>
		//定义组件
		var Home = {
				template : "<h3>我是主页</h3>"
		}
		var News = {
				template : "<h3>我是新闻页</h3>"
		}
		//设置路由
		var routes = [
				{path:'/home',component:Home},
				{path:'/news',component:News},
				{path:'*', redirect:'/home'}
		];
		//创建路由
		var router = new VueRouter({
			routes : routes
		});
		//挂载路由到Vue上
		new Vue({
			router :　router,
			el:'#box'
		});
	</script>
   3、为选中项设置样式
   	.router-link-active{
		font-size : 20px;
		color : #f60;
	}
	
   <!--在路由下设置子路由-->
   <style>
	p{
		width : 100px;
		height: 100px;
		opacity : 1;
		background : red;
		margin : 0 auto;
	}
	.router-link-active{
		font-size : 20px;
		color : #f60;
	}
</style>

<!--在路由下配置子路由-->
<body>
	<div id="box">
		<!--定义两个连接-->
		<div>
			<router-link to="/home">主页</router-link>
			<router-link to="/news">新闻页</router-link>
		</div>
		<div>
			<!-- 显示路由 -->
			<router-view></router-view>
		</div>
	</div>
	
	<script>
		//定义组件
		var Home = {
				template : "<h3>我是主页</h3>"
		}
		var News = {
				template : `
				<div>
					<h3>我是新闻页</h3>
					<router-link to="/news/detail">详情页</router-link>
					<!--这里主要是为了显示组件-->
					<router-view></router-view>
				</div>`
		}
		var Detail = {
				template : "<h3>我是详情页</h3>"
		}
		//设置路由
		var routes = [
				{path:'/home',component:Home},
				{path:'/news',component:News,
					children :　[{   //这里相当于也是一个ｒｏｕｔｅｓ
						path:'detail',component:Detail //这里的detail不能加/
					}]},
				{path:'*', redirect:'/home'}
		];
		//创建路由
		var router = new VueRouter({
			routes : routes
		});
		//挂载路由到Vue上
		new Vue({
			router :　router,
			el:'#box'
		});
	</script>
</body>

<!--点击路由连接的时候获取路径中的数据-->
<body>
	<div id="box">
		<button @click='push'>添加一个路由到堆栈中</button>
		<!--定义两个连接-->
		<div>
			<router-link to="/home">主页</router-link>
			<router-link to="/news">新闻页</router-link>
		</div>
		<div>
			<!-- 显示路由 -->
			<router-view></router-view>
		</div>
	</div>
	
	<script>
		//定义组件
		var Home = {
				template : "<h3>我是主页</h3>"
		}
		var News = {
				template : `
				<div>
					<h3>我是新闻页</h3>
					<!--点击连接的时候获取连接中的值-->
					<router-link to="/news/red/age/10">red</router-link>
					<router-link to="/news/green/age/9">green</router-link>
					<router-link to="/news/black/age/16">black</router-link>
					<router-view></router-view>
				</div>`
		}
		var Detail = {
				<!--获取：中的值-->
				template : `<h3>我是{{$route.params}}</h3>`
		}
		//设置路由
		var routes = [
				{path:'/home',component:Home},
				{path:'/news',component:News,
					children :　[{   //这里相当于也是一个ｒｏｕｔｅｓ
						path:':detail/age/:age',component:Detail //:说明将这个位置的值加入到param中
					}]},
				{path:'*', redirect:'/home'}
		];
		//创建路由
		var router = new VueRouter({
			routes : routes
		});
		//挂载路由到Vue上
		new Vue({
			router :　router,
			el:'#box',
			methods:{
				push(){
					routes.push({path:'news'});//点击按钮的时候跳转到这个路由并把这个路由添加到堆栈中，类似android中的回
					//退栈中
				}
			}
		}).$amount('#box');
	</script>
</body>

<!--设置路由跳转并且添加到history中、配合transition设置动画-->
<body>
	<div id="box">
		<!--定义两个连接-->
		<div>
			<router-link to="/home">主页</router-link>
			<router-link to="/news">新闻页</router-link>
		</div>
		<div>
			<!--使用动画、只需要使用transition包裹、声明两个class即可 -->
			<transition enter-active-class="animated bounceInLeft" leave-active-class="animated bounceOutRight">
				<!-- 显示路由 -->
				<router-view></router-view>
			</transition>
		</div>
	</div>
	
	<script>
		//定义组件
		var Home = {
				template : "<h3>我是主页</h3>"
		}
		var News = {
				template : `
				<div>
					<h3>我是新闻页</h3>
					<!--点击连接的时候获取连接中的值-->
					<router-link to="/news/red/age/10">red</router-link>
					<router-link to="/news/green/age/9">green</router-link>
					<router-link to="/news/black/age/16">black</router-link>
					<router-view></router-view>
				</div>`
		}
		var Detail = {
				<!--获取：中的值-->
				template : `<h3>我是{{$route.params}}</h3>`
		}
		//设置路由
		var routes = [
				{path:'/home',component:Home},
				{path:'/news',component:News,
					children :　[{   //这里相当于也是一个ｒｏｕｔｅｓ
						path:':detail/age/:age',component:Detail //:说明将这个位置的值加入到param中
					}]},
				{path:'*', redirect:'/home'}
		];
		//创建路由
		var router = new VueRouter({
			routes : routes
		});
		//挂载路由到Vue上
		new Vue({
			router :　router,
			el:'#box'
		});
	</script>
</body>
7.vue-loader结合路由 
8.loader的顺序问题 
智能社：Javascript之vue.JS(七）    
1.bootstrap与vue2.0 
2.Element-UI的全局使用 
3.Element-UI的按需使用 
4.结合less的使用 
5.axios的简单使用 
6.Mint-ui的使用 
智能社：Javascript之vue.JS(八） 
1.vue2.0自定义全局组件 
2.use使用 
智能社：Javascript之vue.JS(九） 
1.vuex的讲解以及实例 
智能社：Javascript之vue.JS(十）        
1.vue2.0仿手机新闻项目 
	vue init webpack-simple vue-new-project
智能社：Javascript之vue.JS(十一） 
1.总结 
 
