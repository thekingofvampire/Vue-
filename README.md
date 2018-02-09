# Vue-
写小的demo的时候  使用nodejs的express框架处理请求的时候出现了跨域的问题

  
使用vue-cli快速创建的项目里 ，config/index.js里面的dev字段里有proxyTable ，这个就是用来解决跨域的，当然新建的项目里面这是一个空对象，为了解决跨域，我们只需要添加将其改为

    proxyTable: {
      '/*': {
        target: url,
        changeOrigin: true,
        pathRewrite: {
          '^/*': '/*'
        }
      }
    },
    
    
在前端我们的vue项目里面 就可以直接使用axios来进行跨域请求了（这里的this.$Axios 是在main.js里面 Vue.prototype.$Axios = axios）;

			this.$Axios.get('/api/user?id=1').then(response => {
				console.log(response.data);
			});
			var newUserInfo = {
				userName: 'n',
				phone: '13',
				email: '12',
				emailPwd: '22',
				kindleEmail: 'asd'
			};
			this.$Axios.post('/api/post', newUserInfo).then(response => {
				console.log(response.data);
			});
无论是get请求还是post请求  都不会出现跨域的问题了
