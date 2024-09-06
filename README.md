- 👋 Hi, I’m @ugurluin
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
ugurluin/ugurluin is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
# Revert the plot to the previous version with the slightly thicker original pink and cyan lines

# Create a figure and axis
fig, ax1 = plt.subplots(figsize=(6, 12))

# Display the core sample image with the reversed depth axis
ax1.imshow(img, extent=[2.1, 2.6, new_depths_03.max(), new_depths_03.min()], aspect='auto')

# Plot the averaged density data using the original slightly thicker pink line
ax2 = ax1.twiny()  # Create a twin Axes sharing the y-axis
ax2.plot(interpolated_density_03, new_depths_03, color='#FF69B4', linewidth=2, label='Density')  # Original pink
ax2.set_xlim(2.2, 2.7)  # Keep the density line to the right

# Plot the averaged Mean Zeff data with a slightly thicker cyan line as a continuous line
ax3 = ax1.twiny()  # Create another twin Axes sharing the y-axis
ax3.spines['top'].set_position(('outward', 60))  # Move the Zeff axis upwards to separate it from the density axis
ax3.plot(interpolated_zeff_03, new_depths_03, color='#00FFFF', linewidth=2, linestyle='-', label='Mean Zeff')  # Thicker cyan, continuous
ax3.set_xlim(interpolated_zeff_03.min() + 0.2, interpolated_zeff_03.max() + 0.2)  # Shift the Zeff line to the left

# Invert the y-axis so that depth increases visually upwards but data remains correct
ax1.invert_yaxis()
ax2.invert_yaxis()
ax3.invert_yaxis()

# Remove gridlines
ax1.grid(False)
ax2.grid(False)
ax3.grid(False)

# Label the axes
ax1.set_xlabel('Core Image')
ax2.set_xlabel('Density (g/cm³)')
ax3.set_xlabel('Mean Zeff')
ax1.set_ylabel('Depth (m)')

# Add legends for both lines slightly higher above the image area with a larger font size
fig.legend(loc='upper center', bbox_to_anchor=(0.5, 1.03), ncol=2, fontsize=12)

# Show the plot
plt.show()
