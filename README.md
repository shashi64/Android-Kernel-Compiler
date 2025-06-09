# Compile Android Kernel

This GitHub Action workflow allows you to compile an Android kernel using a specified repository, branch, defconfig, and architecture. It supports optional use of `ccache` for faster builds and allows custom environment variables.


## 📥 Inputs

| Name              | Description                                | Required | Default                                                                 |
|-------------------|--------------------------------------------|----------|-------------------------------------------------------------------------|
| `kernel_clone_cmd`| Git clone command to fetch the kernel repo | ✅ Yes   | `https://github.com/xiaomi-msm8953-devs/android_kernel_xiaomi_msm8953.git` |
| `kernel_branch`   | Kernel branch to checkout and build        | ✅ Yes   | `lineage-22.2`                                                          |
| `kernel_config`   | Defconfig file(s) for the kernel           | ✅ Yes   | `msm8953-perf_defconfig xiaomi/vince.config`                           |
| `arch`            | Target architecture                        | ✅ Yes   | `arm64` <br>Options: `arm64`, `arm`                                    |
| `enable_ccache`   | Enable `ccache` for faster builds          | ❌ No    | `true` <br>Options: `true`, `false`                                    |
| `build_env`       | Additional build environment variables     | ❌ No    |  `O=out PATH=$HOME/clang/bin:$PATH CC="ccache clang" CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=aarch64-linux-gnu- CROSS_COMPILE_ARM32=arm-linux-gnueabi-` |
| `toolchain`       | Path or URL to the Clang/GCC toolchain     | ❌ No    | `https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86/+archive/refs/heads/android12-release/clang-r416183b1.tar.gz` |

## 🛠️ Usage

To run the workflow manually:

1. **Fork** this repository
2. Go to the **Actions** tab in your GitHub repository.
3. Select the **Compile Kernel** workflow.
4. Click **Run workflow**, fill in the input parameters, and click **Run**.

## 📦 Output

The output will include the compiled kernel (zImage/Image.gz-dtb or equivalent)

## 🧰 Notes

- This workflow uses **AOSP Clang** by default to compile the kernel.
- **Not all kernels are compatible with AOSP Clang.** If you encounter build errors, it may be due to incompatibility with this clang you can try again by changing clang. You can get it from the official Android source at:  
  [https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86](https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86) and **Note** copy tar.gz link address as shown in inputs.
- If the kernel source requires device-specific patches, apply them before using this workflow.

---
