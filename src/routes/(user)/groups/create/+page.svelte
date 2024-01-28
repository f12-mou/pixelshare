<script>
  // @ts-nocheck

  import { writable } from "svelte/store";

  const profileImg = writable("");
  const coverImg = writable("");

  function handleFileChange(type, event) {
    const file = event.target.files[0];
    if (file) {
      const imageUrl = URL.createObjectURL(file);
      if (type === "profile") {
        profileImg.set(imageUrl);
      } else if (type === "cover") {
        coverImg.set(imageUrl);
      }
    }
  }

  async function post() {
    alert("Post submitted!"); // Placeholder for actual post submission
  }
</script>

<div
  class="flex flex-col items-center justify-center min-h-screen bg-orange-50 text-gray-900 px-36"
>
  <div class="space-y-4 w-full">
    <!-- Image selection for Cover and Profile Image -->
    <div class="flex gap-4 justify-center items-end">
      <div class="flex-1">
        <label for="cover-file-input" class="cursor-pointer block text-center">
          <div class="p-4 border-2 border-dashed border-gray-600 rounded-lg">
            {#if $coverImg}
              <!-- svelte-ignore a11y-img-redundant-alt -->
              <img
                src={$coverImg}
                alt="Cover Image"
                class="rounded-lg mx-auto"
              />
            {:else}
              <!-- svelte-ignore a11y-missing-attribute -->
              <img src="icons/add-image.png" class="mx-auto mb-2" />
              <span>Select Cover Pic</span>
            {/if}
          </div>
        </label>
        <input
          type="file"
          id="cover-file-input"
          accept="image/*"
          on:change={() => handleFileChange("cover", event)}
          hidden
        />
      </div>
      <div class="flex-1">
        <label
          for="profile-file-input"
          class="cursor-pointer block text-center"
        >
          <div class="p-4 border-2 border-dashed border-gray-600 rounded-lg">
            {#if $profileImg}
              <!-- svelte-ignore a11y-img-redundant-alt -->
              <img
                src={$profileImg}
                alt="Profile Image"
                class="rounded-lg mx-auto"
              />
            {:else}
              <img
                src="icons/add-image.png"
                class="mx-auto mb-2"
                alt="Missing here"
              />
              <span>Select Profile Pic</span>
            {/if}
          </div>
        </label>
        <input
          type="file"
          id="profile-file-input"
          accept="image/*"
          on:change={() => handleFileChange("profile", event)}
          hidden
        />
      </div>
    </div>

    <!-- Group Name input -->
    <input
      type="text"
      placeholder="Enter Group Name"
      class="w-full p-2 bg-orange-100 border border-white-300 rounded-md text-black"
    />

    <!-- Group Bio input -->
    <textarea
      placeholder="Write a short bio for the group"
      class="w-full p-2 bg-orange-100 border border-white-300 rounded-md text-black"
    ></textarea>

    <!-- Submit button -->
    <div class="text-center">
      <button
        on:click={post}
        class="px-24 py-3 bg-orange-200 border-2 border-orange-300 hover:bg-orange-300 rounded-md"
        >Create Group</button
      >
    </div>
  </div>
</div>