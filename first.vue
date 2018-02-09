<template>
	<div>
      <div v-if="show">
         <input type="text" placeholder="NICKNAME" v-model="nickname" @keyup.13="confirm" autofocus>
      </div>
      <div v-else>
         <ul>
            <li v-for="(item,key) in items" :key="key">{{item}}</li>
         </ul>
         <input type="text" v-model="inpval" @keyup.13="btnclick" autofocus="autofocus">
         <button @click="btnclick">发送</button>
      </div>
	</div>
</template>
<script>
export default {
	data() {
		return {
			items: [],
			inpval: null,
			show: true,
			nickname: null,
			id: '',
			val: ''
		};
	},
	methods: {
		btnclick() {
			// console.log(this.$Axios);
			console.log(this.$store.state);
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
			var me = this;
			me.items.push(me.nickname + '：' + me.inpval);
			me.inpval = '';
			socket.on('news', function(data) {
				console.log('执行了');
				socket.emit('socket', { msg: me.inpval });
				// console.log('data');
				// console.log(data);
				if (data.code == 200) {
					// console.log(11111);
					me.inpval = '';
				}
			});
		},
		confirm() {
			this.show = !this.show;
		}
	}
};
</script>
<style lang="less" scoped>

</style>

