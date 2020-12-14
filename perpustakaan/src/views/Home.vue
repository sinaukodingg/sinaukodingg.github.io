<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src

@Component({
  components: {
    HelloWorld,
  },
})
export default class Home extends Vue {
  interface User {
    id: number;
    nama: string;
    role: Role;
  }
  enum Role{
    ADMIN = "ADMIN",
    MAHASISWA = "MAHASISWA"
  }
  abstract class BaseUser implements User{
    public id: number = 0;
    public nama: string = "";
    public abstract role: Role;
    public toString(): string{
      return JSON.stringify(this);
    }
  }
  class mahasiswa extends BaseUser{
    public NRP: number = 0;
    public role: Role = Role.Mahasiswa;
  }
  class admin extends BaseUser{
    public NIP: number = 0;
    public role: Role = Role.Admin;
  }
  class UserService{
    private admin: admin;
    private mahasiswa: mahasiswa;
    constructor(admin: admin, mahasiswa: mahasiswa){
      this.admin = admin;
      this.mahasiswa = mahasiswa;
    }
    public createLog(): void{
      console.log("admin", this.admin.toString());
      console.log("mahasiswa", this.mahasiswa.toString());
    }
  }
}
</script>
