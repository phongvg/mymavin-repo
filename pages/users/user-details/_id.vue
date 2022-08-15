<script>
import vue2Dropzone from "vue2-dropzone";
import { usersData } from "../data";
/**
 * Product-create component
 */
export default {
  head() {
    return {
      title: `${this.title} | My Mavin`,
    };
  },
  components: {
    vueDropzone: vue2Dropzone,
  },
  asyncData({ params }) {
    const userDetail = usersData.find((user) => String(user.id) === params.id);
    return {
      userDetail,
    };
  },
  created() {
    this.userName = this.userDetail.username;
    this.fullname = this.userDetail.name;
    this.gmail = this.userDetail.gmail;
  },
  data() {
    return {
      title: "Chi tiết tài khoản",
      items: [
        {
          text: "My Mavin",
        },
        {
          text: "Người dùng",
        },
        {
          text: "Chi tiết tài khoản",
          active: true,
        },
      ],
      dropzoneOptions: {
        url: "https://httpbin.org/post",
        thumbnailWidth: 150,
        maxFilesize: 0.5,
        headers: {
          "My-Awesome-Header": "header value",
        },
        previewTemplate: this.template(),
      },
    };
  },
  methods: {
    template: function () {
      return ` <div class="dropzone-previews mt-3">
            <div class="card mt-1 mb-0 shadow-none border">
                <div class="p-2">
                    <div class="row align-items-center">
                        <div class="col-auto">
                            <img data-dz-thumbnail src="#" class="avatar-sm rounded bg-light" alt="">
                        </div>
                        <div class="col pl-0">
                            <a href="javascript:void(0);" class="text-muted font-weight-bold" data-dz-name></a>
                            <p class="mb-0" data-dz-size></p>
                        </div>
                        <div class="col-auto">
                            <!-- Button -->
                            <a href="" class="btn btn-link btn-lg text-muted" data-dz-remove>
                                <i class="fe-x"></i>
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        `;
    },
  },
  middleware: "router-auth",
};
</script>

<template>
  <div>
    <PageHeader :title="title" :items="items" />

    <div class="row">
      <div class="col-lg-12">
        <div class="card">
          <div class="card-body">
            <nuxt-link to="#" class="btn btn-danger mb-2"
              ><i class="mdi mdi-checkbox-marked-circle mr-1"></i>Duyệt tài
              khoản
            </nuxt-link>
            <form>
              <h4 class="header-title">Thông tin chung</h4>
              <p class="sub-header">Những trường có dấu * là bắt buộc.</p>

              <div>
                <div class="row">
                  <div class="col-lg-6">
                    <div class="form-group mb-3">
                      <label for="user-name">
                        Tên tài khoản
                        <span class="text-danger">*</span>
                      </label>
                      <input
                        type="text"
                        id="user-name"
                        class="form-control"
                        v-model="userName"
                      />
                    </div>
                  </div>
                  <div class="col-lg-6">
                    <div class="form-group mb-3">
                      <label for="user-type">
                        Loại tài khoản
                        <span class="text-danger">*</span>
                      </label>
                      <select class="form-control select2" id="user-type">
                        <option>Lựa chọn</option>
                        <option value="SH1">Admin cấp tập đoàn</option>
                        <option value="SH2">Admin cấp đơn vị</option>
                        <option value="SH3">Nhân viên</option>
                      </select>
                    </div>
                  </div>
                </div>
                <div class="row">
                  <div class="col-lg-6">
                    <div class="form-group mb-3">
                      <label for="user-password">
                        Mật khẩu
                        <span class="text-danger">*</span>
                      </label>
                      <input
                        type="password"
                        id="user-password"
                        class="form-control"
                        v-model="userPassword"
                      />
                    </div>
                  </div>
                </div>
                <div class="row">
                  <div class="col-lg-6">
                    <div class="form-group mb-3">
                      <label for="fullname">
                        Tên người dùng
                        <span class="text-danger">*</span>
                      </label>
                      <input
                        type="text"
                        id="fullname"
                        class="form-control"
                        v-model="fullname"
                      />
                    </div>
                  </div>
                </div>
                <div class="row">
                  <div class="col-lg-6">
                    <div class="form-group mb-3">
                      <label for="email">
                        Email
                        <span class="text-danger">*</span>
                      </label>
                      <input
                        type="text"
                        id="email"
                        class="form-control"
                        v-model="gmail"
                      />
                    </div>
                  </div>
                </div>
              </div>

              <ul class="pager wizard mb-0 list-inline text-right mt-3">
                <li class="next list-inline-item"></li>
              </ul>

              <h4 class="header-title">Ảnh đại diện</h4>
              <p class="sub-header">Tải ảnh lên</p>

              <vue-dropzone
                id="dropzone"
                ref="myVueDropzone"
                :use-custom-slot="true"
                :options="dropzoneOptions"
              >
                <div>
                  <img
                    v-if="userDetail.profile"
                    :src="userDetail.profile"
                    alt=""
                    class="rounded mr-3"
                    height="111"
                  />
                </div>
                <div class="dz-message needsclick">
                  <i class="h1 text-muted ri-upload-cloud-2-line"></i>
                  <h3>Kéo ảnh vào hoặc bấm vào đây để tải ảnh lên.</h3>
                  <span class="text-muted font-13">
                    (This is just a demo dropzone. Selected files are
                    <strong>not</strong> actually uploaded.)
                  </span>
                </div>
              </vue-dropzone>
              <div class="form-group text-right m-b-0" style="margin-top: 20px">
                <button class="btn btn-primary" type="submit">
                  Sửa thông tin
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
    <!-- end row -->
  </div>
</template>
