<template>
<div>
    <Navbar/>
    <main role="main">
      <div class="container marketing">
<h2 class="eventSection text-center mb-5">報名表單明細</h2>

<div class="table eventDetail container">
  <div class="row">
          <table id="actDetail">

              <tr>
                <th>活動名稱</th>
                <td>{{ orderConfirm.order[0].p_id.p_id.title }}</td>
              </tr>

                <tr >
                <th>活動日程</th>
                <td>{{ orderConfirm.order[0].p_id.date }}</td>
              </tr>

              <tr>
                <th>活動時間</th>
                <td>{{ orderConfirm.order[0].p_id.p_id.time }}</td>
              </tr>  

                <tr>
                <th>活動費用</th>
                <td>NT${{ orderConfirm.order[0].p_id.price }}</td>
              </tr> 

                <tr >
                <th>姓名</th>
                <td>{{ userConfirm[0].name }}</td>
              </tr>

              <tr >
                <th>LINE ID</th>
                <td>{{ userConfirm[0].lineId}}</td>
              </tr>                             

              <tr >
                <th>LINE 名稱</th>
                <td>{{ userConfirm[0].lineName}}</td>
              </tr> 

              <tr >
                <th>性別</th>
                <td>{{ userConfirm[0].gender}}</td>
              </tr> 

              <tr >
                <th>出生年月日</th>
                <td>{{ userConfirm[0].birth}}</td>
              </tr> 

              <tr >
                <th>國籍</th>
                <td>{{ userConfirm[0].country }}</td>
              </tr> 

              <tr >
                <th>血型</th>
                <td>{{ userConfirm[0].blood }}</td>
              </tr> 

              <tr >
                <th>身份證字號</th>
                <td>{{ userConfirm[0].identityNumber }}</td>
              </tr> 

              <tr >
                <th>連絡電話</th>
                <td>{{ userConfirm[0].cellNumber }}</td>
              </tr> 

              <tr >
                <th>地址</th>
                <td>{{ userConfirm[0].address }}</td>
              </tr> 

              <tr >
                <th>緊急連絡人</th>
                <td>{{ userConfirm[0].emergency }}</td>
              </tr> 

              <tr >
                <th>緊急連絡人關係</th>
                <td>{{ userConfirm[0].emergeRelationship }}</td>
              </tr> 


              <tr >
                <th>飲食習慣</th>
                <td>{{ userConfirm[0].eatingHabits }}</td>
              </tr> 

              <tr >
                <th>登山經驗</th>
                <td>{{ userConfirm[0].climbExperience }}</td>
              </tr> 

              <tr >
                <th>匯款金額</th>
                <td>NT${{ userConfirm[0].paidprice }}</td>
              </tr> 

              <tr >
                <th>匯款日期</th>
                <td>{{ userConfirm[0].paidate }}</td>
              </tr> 

              <tr >
                <th>相關疑問</th>
                <td>{{ userConfirm[0].message }}</td>
              </tr>

          </table>
        </div>
          </div>

      </div>
    </main>

</div>
</template>

<script>
import Navbar from '../Navbar'
import store from '@/store'
import Axios from 'axios'
export default {
  name: 'UserConfrim',
  components: {
    Navbar,
    },
  data () {
    return {
      orderConfirm:{
        order:[{
          p_id:{
          p_id:{name:'',
          }
        }
        }]
      
      },
      userConfirm:[{
            name:'',
            lineId:'',
            lineName:'',
            gender:'',
            birth:'',
            country:'',
            blood:'',
            identityNumber:'',
            cellNumber:'',
            email: '',
            address:'',
            emergency:'',
            emergeRelationship:'',
            eatingHabits:'',
            disease:'',
            climbExperience:'',
            paidprice:'',
            paidate:'',
            message:''
        
      }]
    }
  },
  computed: {
    user () {
      return store.state.user
    },
    products() {
      return store.state.products; 
    },
    newplanswiper(){
      return store.state.newplans
    },
  },

    methods: {  
       // 取得訂單及行程資料
        getOrder() {
        const api = `${process.env.VUE_APP_API}`+ '/users/order/'+ `${this.user.id}`
        Axios.get(api).then((response) => {
        if(response.data.success){
        this.orderConfirm = response.data.result
          }console.log('已取得訂單資料',response.data.result)
        })
        },
        // 取得報名資料
        getOrderUserDetails() {
        const api = `${process.env.VUE_APP_API}`+ '/userdetails/' + `${this.user.id}`
        Axios.get(api).then((response) => {
        if(response.data.success){
        this.userConfirm = response.data.result
          }console.log('已取得報名資料',response.data.result)
        })
        },
    },
    created() {
      this.getOrder();
      this.getOrderUserDetails()
    },
}
</script>
